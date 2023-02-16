<template>
  <div>
    <img :src="product.image" class="room-img">
    <h4 @click="$emit('openModal', product.id);" class="cursor">{{product.title}}</h4>
    <p>{{product.price}} 만원</p>
  </div>
</template>

<script>
export default {
    name: "isCard",
    props: {
        product: Object,
    },
}
</script>

<style>
    .room-img {
        width: 100%;
        margin-top: 40px;
    }
</style>