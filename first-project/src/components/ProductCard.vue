<template>
  <div>
    <img :src="product.image" class="room-img" />
    <h3 @click="$emit('handleTitle', product.id)">
      {{ product.title }}
    </h3>
    <p>{{ product.content }}</p>
    <p>{{ product.price }}만원</p>
    <button @click="$emit('handleButton')">추천하기</button>
    <span>추천수 : {{ product.buttonCount }}</span>
  </div>
</template>

<script>
export default {
  name: "ProductCard",
  props: {
    product: Object,
    clicked: Number,
    hidden: Boolean,
  },
};
</script>

<style></style>
