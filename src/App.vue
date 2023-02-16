<template>
  <!-- 모달 -->
  <transition name="fade">
    <Modal @closeModal="isOpenModal=false;" 
      :products="products" 
      :isOpenModal="isOpenModal" 
      :currentProductId="currentProductId" 
      />
  </transition>

  <!-- 메뉴 -->
  <div class="menu">
    <a v-for="(menuItem, index) of menuList" :key="index">{{menuItem}}</a>
  </div>

  <!-- 할인 문구 -->
  <Discount :accountPercent="accountPercent" />

  <button @click="priceSort">가격 낮은 순 정렬</button>
  <button @click="priceReverseSort">가격 높은 순 정렬</button>
  <button @click="sortBack">되돌리기</button>

  <!-- 원룸 카드 목록 -->
  <Card @openModal="isOpenModal=true; currentProductId=$event;" v-for="product of products" :key="product.id" :product="product" />

</template>

<script>
  import data from "./assets/oneroom";
  import Discount from "./Discount.vue";
  import Modal from "./Modal.vue";
  import Card from "./Card.vue";

  export default {
    name: 'App',
    data() {
      return {
        productOriginal: [...data],
        products: data,
        menuList: ["Home", "Shop", "About"],
        reportCount: [0,0,0],
        isOpenModal: false,
        currentProductId: null,
        accountPercent: 30,
      };
    },
    methods: {  
      priceSort() {
        this.products.sort((a, b)=> {
          return a.price - b.price;
        });
      },
      priceReverseSort() {
        this.products.sort((a, b)=> {
          return b.price - a.price;
        });
      },
      sortBack() {
        this.products = [...this.productOriginal];
      },
    },
    components: {
      Discount,
      Modal,
      Card,
    },
    mounted() {
      const timer = setInterval(()=> {
        this.accountPercent--;
      }, 1000);
      setTimeout(()=> {
        clearInterval(timer);
      }, 30000);
    },
  }
</script>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
  }

  body {
    margin: 0;
  }
  div {
    box-sizing: border-box;
  }
  .cursor {
    cursor: pointer;
  }

  .black-bg {
    width: 100%;
    height: 100%;
    background: rgba(0,0,0,0.5);
    position: fixed; padding: 20px;
  }
  .white-bg {
    width: 100%; background: white;
    border-radius: 8px;
    padding: 20px;
  }

  .menu {
    background: darkslateblue;
    padding: 15px;
    border-radius: 5px;
  }
  .menu a {
    color: white;
    padding: 10px;
  }

  .fade-enter-from {
    opacity: 0;
  }
  .fade-enter-active {
    transition: all 1s;
  }
  .fade-enter-to {
    opacity: 1;
  }
  .fade-leave-from {
    opacity: 1;
  }
  .fade-leave-active {
    transition: all 1s;
  }
  .fade-leave-to {
    opacity: 0;
  }
</style>
