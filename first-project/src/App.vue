<template>
  <div class="navigation">
    <a v-for="(menu, i) in menuName" :key="i">{{ menu }}</a>
    <!-- vue의 반복문 : v-for="변수명 in 자료이름" :key="자료이름" -->
    <!-- 변수는 각각의 아이템이 된다 -->
    <!-- 변수는 두개까지 만들 수 있고, 오른쪽 변수는 1씩 증가하는 정수이다. 오른쪽 변수를 key값으로 활용한다. -->
  </div>

  <section class="section">
    <div>
      <h3>{{ products[0] }}</h3>
      <p>{{ prices[0] }}만원</p>
      <button @click="buttonCount[0]++">허위매물신고</button>
      <!-- 이벤트리스너 사용하기 : v-on:click=" " 혹은 @click=" " -->
      <span>신고 수 : {{ buttonCount[0] }}</span>
    </div>
    <div>
      <h3>{{ products[1] }}</h3>
      <p>{{ prices[1] }}만원</p>
      <button @click="buttonCount[1]++">허위매물신고</button>
      <span>신고 수 : {{ buttonCount[1] }}</span>
    </div>
    <div>
      <h3>{{ products[2] }}</h3>
      <p>{{ prices[2] }}만원</p>
      <button @click="buttonCount[2]++">허위매물신고</button>
      <span>신고 수 : {{ buttonCount[2] }}</span>
    </div>
  </section>

  <section class="section">
    <h4 :style="style1">위 내용 반복문 사용해서 다시 만들기</h4>
    <div v-for="(product, i) in productList" :key="i">
      <h3>{{ product.name }}</h3>
      <p>{{ product.price }}만원</p>
      <button @click="product.buttonCount++">허위매물신고</button>
      <span>신고 수 : {{ product.buttonCount }}</span>
    </div>
  </section>
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
      buttonCount: [0, 0, 0],
      // 반복문용 데이터
      productList: [
        { name: "역삼동원룸", price: 50, buttonCount: 0 },
        { name: "천호동원룸", price: 60, buttonCount: 0 },
        { name: "자양동원룸", price: 100, buttonCount: 0 },
      ],
    };
  },
  methods: {
    addCount() {
      this.buttonCount++;
      // 함수를 만들어서 사용하고 싶을떄 methos안에 함수를 만들어서 사용
      // 데이터를 가져다 쓰고싶을때 앞에 this 사용하기
    },
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
  padding: 40px;
}

button {
  margin-right: 4px;
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

.section {
  padding: 40px;
  border-radius: 8px;
  background-color: #f2f2f2;
  margin-bottom: 40px;
}
</style>
