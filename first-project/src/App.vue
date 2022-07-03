<template>
  <!-- 부모가 가진 데이터를 자식컴포넌트가 사용하고 싶으면 props로 전해주기 -->
  <DetailModal :roomData="roomData" :clicked="clicked" :hidden="hidden" />

  <nav class="navigation">
    <a v-for="(menu, i) in menuName" :key="i">{{ menu }}</a>
    <!-- vue의 반복문 : v-for="변수명 in 자료이름" :key="자료이름" -->
    <!-- 변수는 각각의 아이템이 된다 -->
    <!-- 변수는 두개까지 만들 수 있고, 오른쪽 변수는 1씩 증가하는 정수이다. 오른쪽 변수를 key값으로 활용한다. -->
  </nav>

  <DiscountBanner />

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

  <h4 :style="redText">위 내용 반복문 사용해서 하단에 다시 생성</h4>

  <section class="section">
    <div v-for="(product, i) in roomData" :key="i">
      <img :src="product.image" class="room-img" />
      <h3
        @click="
          hidden = true;
          clicked = product.id;
        "
      >
        {{ product.title }}
      </h3>
      <p>{{ product.content }}</p>
      <p :style="redText">{{ product.price }}만원</p>
      <button @click="product.buttonCount++">추천하기</button>
      <span>추천수 : {{ product.buttonCount }}</span>
    </div>
  </section>
</template>

<script>
import roomData from "./assets/roomData.js";
import DiscountBanner from "./components/DiscountBanner.vue";
import DetailModal from "./components/DetailModal.vue";

export default {
  name: "App",
  data() {
    return {
      // 자주 바뀌는 데이터는 따로 담아서 데이터바인딩
      products: ["역삼동원룸", "천호동원룸", "마포구원룸"],
      prices: [50, 60, 100],
      menuName: ["Home", "Rooms", "About"],
      // HTML 속성도 데이터바인딩이 가능하다. HTML태그 안에 사용 시 앞에 콜론 붙일 것
      redText: "color: tomato",
      buttonCount: [0, 0, 0],
      // UI 상태 컨트롤
      // 리액트로 말하자면 useState의 기능
      hidden: false,
      // 데이터 파일 import
      roomData: roomData,
      // 모달 내 각 아이템 데이터 노출하기
      clicked: 0,
    };
  },
  methods: {
    // 함수를 만들어서 사용하고 싶을떄 methos안에 함수를 만들어서 사용
    // 데이터를 가져다 쓰고싶을때 앞에 this 사용하기
  },
  components: {
    // 만들어둔 컴포넌트 파일을 import 해와서 components 오브젝트에 등록 (key: value)
    DiscountBanner,
    DetailModal,
  },
};
</script>

<style>
body {
  margin: 0;
  padding: 0;
  border: 0;
  text-align: center;
  box-sizing: border-box;
}

button {
  margin-right: 6px;
}

.navigation {
  background-color: tomato;
  padding: 16px;
}

.navigation a {
  font-size: 24px;
  font-weight: 700;
  color: white;
  padding: 8px 16px;
}

.section {
  padding: 40px;
  background-color: #f2f2f2;
  margin-bottom: 40px;
}

.section div {
  margin-bottom: 24px;
}

.section div h3:hover {
  cursor: pointer;
  opacity: 0.5;
}

.room-img {
  width: 400px;
  height: 260px;
  border-radius: 8px;
}
</style>
