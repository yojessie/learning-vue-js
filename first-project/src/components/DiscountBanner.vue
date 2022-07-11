<template>
  <div class="banner">
    <h3>💛 지금 결제하면 {{ percent }}% 할인 💛</h3>
  </div>
</template>

<script>
export default {
  name: "DiscountBanner",
  props: {
    percent: Number,
  },
};
</script>

<style>
.banner {
  background-color: floralwhite;
  color: tomato;
  padding: 16px;
  margin-bottom: 40px;
}
</style>
