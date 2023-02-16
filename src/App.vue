<template>
  <!-- 모달 -->
  <Modal @closeModal="isOpenModal=false;" :products="products" :isOpenModal="isOpenModal" :currentProductId="currentProductId" />

  <!-- 메뉴 -->
  <div class="menu">
    <a v-for="(menuItem, index) of menuList" :key="index">{{menuItem}}</a>
  </div>

  <!-- 할인 문구 -->
  <Discount />

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
        products: data,
        menuList: ["Home", "Shop", "About"],
        reportCount: [0,0,0],
        isOpenModal: false,
        currentProductId: null,
      };
    },
    methods: {
    },
    components: {
      Discount,
      Modal,
      Card,
    }
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
</style>
