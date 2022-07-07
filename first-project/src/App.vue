<template>
  <!-- 부모가 가진 데이터를 자식컴포넌트가 사용하고 싶으면 props로 전해주기 -->
  <!-- Animation을 줄때, :class="{클래스명 : 조건}" 을 넣어주면, 조건값이 참일때만 클래스를 붙여준다. -->
  <!-- <div class="modal-start" :class="{ 'modal-end': hidden }"> -->
  <!-- 위와 같이 쓸 수도 있지만, transition을 줄 수도 있다. -->
  <transition name="fade">
    <DetailModal
      @handleModal="hidden = false"
      :roomData="roomData"
      :clicked="clicked"
      :hidden="hidden"
    />
  </transition>

  <nav class="navigation">
    <a v-for="(menu, i) in menuName" :key="i">{{ menu }}</a>
    <!-- vue의 반복문 : v-for="변수명 in 자료이름" :key="자료이름" -->
    <!-- 변수는 각각의 아이템이 된다 -->
    <!-- 변수는 두개까지 만들 수 있고, 오른쪽 변수는 1씩 증가하는 정수이다. 오른쪽 변수를 key값으로 활용한다. -->
  </nav>

  <DiscountBanner v-if="showBanner" />

  <section class="section">
    <div class="button-group">
      <button @click="sortLow">낮은 가격순 정렬</button>
      <button @click="sortHigh">높은 가격순 정렬</button>
      <button @click="sortText">이름순 정렬</button>
      <button @click="sortReset">초기화</button>
    </div>
    <ProductCard
      @handleTitle="
        hidden = true;
        clicked = $event;
      "
      @handleButton="product.buttonCount++"
      :product="roomData[i]"
      v-for="(product, i) in roomData"
      :key="i"
    />
    <!-- 자식 컴포넌트에서 보낸 데이터 가져올때는 $event -->
  </section>
</template>

<script>
import roomData from "./assets/roomData.js";
import DiscountBanner from "./components/DiscountBanner.vue";
import DetailModal from "./components/DetailModal.vue";
import ProductCard from "./components/ProductCard.vue";

export default {
  name: "App",
  data() {
    return {
      // 자주 바뀌는 데이터는 따로 담아서 데이터바인딩
      products: ["역삼동원룸", "천호동원룸", "마포구원룸"],
      prices: [50, 60, 100],
      menuName: ["Home", "Rooms", "About"],
      buttonCount: [0, 0, 0],
      // UI 상태 컨트롤
      // 리액트로 말하자면 useState의 기능
      hidden: false,
      showBanner: true,
      // 데이터 파일 import
      // array, object 데이터의 별개 사본을 만들기 [...arr] : spread operator
      roomDataOrigin: [...roomData],
      roomData: roomData,
      // 모달 내 각 아이템 데이터 노출하기
      clicked: 0,
    };
  },
  methods: {
    // 함수를 만들어서 사용하고 싶을떄 methos안에 함수를 만들어서 사용
    // 데이터를 가져다 쓰고싶을때 앞에 this 사용하기 📌
    sortLow() {
      this.roomData.sort(function (a, b) {
        return a.price - b.price;
      });
      // sort함수 동작원리 확인 필요. sort함수는 원본데이터를 변형시키므로, 원본을 별도 저장해놔야함.
    },
    sortHigh() {
      this.roomData.sort(function (a, b) {
        return b.price - a.price;
      });
    },
    sortText() {
      this.roomData.sort(function (a, b) {
        const upperCaseA = a.title.toUpperCase();
        const upperCaseB = b.title.toUpperCase();

        if (upperCaseA > upperCaseB) return 1;
        if (upperCaseA < upperCaseB) return -1;
        if (upperCaseA === upperCaseB) return 0;
      });
    },
    sortReset() {
      this.roomData = [...this.roomDataOrigin];
      // arr자료 = arr자료 의 방식으로 값을 재할당하면, array 자료의 경우 값을 '공유'해달라는 의미가 된다.
      // 따라서 재할당 하려는 값을 다시 사본으로 만들어서 재할당한다.
    },
  },
  // lifecycle hook
  // beforeCreate()
  // created()
  // beforeMount()
  // mounted() ...
  // ajax 요청은 주로 created 나 mounted 에 hook
  mounted() {
    setTimeout(() => {
      this.showBanner = false;
      // arrow function 필요
    }, 2000);
  },
  components: {
    // 만들어둔 컴포넌트 파일을 import 해와서 components 오브젝트에 등록 (key: value)
    DiscountBanner,
    DetailModal,
    ProductCard,
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

.button-group {
  margin-bottom: 24px;
}

.room-img {
  width: 400px;
  height: 260px;
  border-radius: 8px;
}

.modal-start {
  opacity: 0;
  transition: opacity 300ms ease-in-out;
}

.modal-end {
  opacity: 1;
}

/* vue의 transition animation */
.fade-enter-from {
  transform: translateY(-2000px);
}
.fade-enter-active {
  transition: transform 500ms ease-in-out;
}
.fade-enter-to {
  transform: translateY(0px);
}
.fade-leave-from {
  transform: translateY(0px);
}
.fade-leave-active {
  transition: transform 500ms ease-in-out;
}
.fade-leave-to {
  transform: translateY(-2000px);
}
</style>
