<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <div>
    <h4 :style="style1">{{ products[0] }}</h4>
    <p>{{ prices[0] }}만원</p>
  </div>
  <div>
    <h4>{{ products[1] }}</h4>
    <p>{{ prices[1] }}만원</p>
  </div>
  <div>
    <h4>{{ products[2] }}</h4>
    <p>{{ prices[2] }}만원</p>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      // 자주 바뀌는 데이터는 따로 담아서 데이터바인딩
      products: ["역삼동원룸", "천호동원룸", "마포구원룸"],
      prices: [50, 60, 100],
      // HTML 속성도 데이터바인딩이 가능하다. HTML태그 안에 사용 시 앞에 콜론 붙일 것
      style1: "color: tomato",
    };
  },
  components: {},
};
</script>

<style>
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
