<template>
  <div class="navigation">
    <a v-for="(menu, i) in menuName" :key="i">{{ menu }}</a>
    <!-- vue의 반복문 : v-for="변수명 in 자료이름" :key="자료이름" -->
    <!-- 변수는 각각의 아이템이 된다 -->
    <!-- 변수는 두개까지 만들 수 있고, 오른쪽 변수는 1씩 증가하는 정수이다. 오른쪽 변수를 key값으로 활용한다. -->
  </div>

  <div>
    <h4>{{ products[0] }}</h4>
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

  <h2 :style="style1">반복문 사용해서 다시 만들기</h2>
  <div v-for="(product, i) in products" :key="i">
    <h4>{{ product }}</h4>
    <p>{{ prices[0] }}만원</p>
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
      menuName: ["Home", "Rooms", "About"],
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
}

.navigation {
  background-color: tomato;
  padding: 16px;
  border-radius: 8px;
  margin-bottom: 24px;
}

.navigation a {
  font-size: 24px;
  font-weight: 700;
  color: white;
  padding: 16px 8px;
}
</style>
