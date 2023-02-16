<template>
  <div class="black-bg" v-if="isOpenModal">
    <div class="white-bg">
      <img :src="products[currentProductId].image">
      <h4>{{products[currentProductId].title}}</h4>
      <p>{{products[currentProductId].content}}</p>
      <input v-model="month">
      <p>{{month}}개월 선택 함 : {{products[currentProductId].price * month}} 만원 </p>
      <button @click="$emit('closeModal');">닫기</button>
    </div>
  </div>
</template>

<script>
export default {
    name: "isModal",
    props: {
        products : Array,
        isOpenModal: Boolean,
        currentProductId: Number,
    },
    data() {
      return {
        month: 1,
      };
    },
    watch: {
      month(data) { 
          if (isNaN(data)) {
            alert('문자 입력 금지');
            this.month = 1;
          }
      }
    },
    beforeUpdate() {
      if (parseInt(this.month)===2) {
        alert('2는 상종 안합니다');
        this.month = 1;
      }
    }
}
</script>

<style>

</style>