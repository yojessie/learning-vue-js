<template>
  <aside class="overlay" v-if="hidden">
    <!-- 조건문을 사용하고 싶을때 v-if 사용, 조건문이 참일때 이 영역을 보여준다. -->
    <!-- v-if : 조건문이 참일때 컴포넌트 보여줌 -->
    <!-- v-else-if : 조건문이 거짓일때 보여줌 -->
    <!-- v-else : 위 내용까지 다 거짓일때 보여줌 -->
    <div class="modal">
      <img :src="roomData[clicked].image" class="room-img" />
      <h2>{{ roomData[clicked].title }}</h2>
      <p>{{ roomData[clicked].content }}</p>
      <!-- <input @input="month = $event.target.value" placeholder="개월수" type="number" /> -->
      <!-- 위 코드를 약어로 사용할수도 있다. -->
      <input v-model.number="month" placeholder="개월수" type="number" />
      <!-- 인풋으로 넘어오는 데이터는 string이 되므로, v-model에 number를 붙여 number로 만들어준다. type을 number로 지정하는것과는 별개 -->
      <p>{{ month }}개월 렌트 : {{ roomData[clicked].price * month }}만원</p>
      <button @click="$emit('handleModal')">닫기</button>
      <!-- 부모에게 데이터를 수정요청 $emit('작명', '데이터') -->
    </div>
  </aside>
</template>

<script>
export default {
  name: "DetailModal",
  data() {
    return {
      month: 1,
      // 데이터의 초기값은 데이터 타입에 맞게 정의해야한다.
    };
  },
  // 사용자가 인풋에 데이터를 입력하는 페이지에서는 데이터를 확인하는 watcher를 사용한다.
  watch: {
    month(data) {
      // month의 데이터를 감시하는 함수가 된다.
      // month라는 데이터가 변화할 때 마다 해당 함수가 실행된다.
      // 해당 함수의 파라미터값은 데이터의 값이 된다. 두번째 파라미터값은 변경전 데이터이다.
      if (data >= 13) {
        alert("최대 렌트 가능 기간은 12개월 입니다.");
        this.month = 12;
      }
      if (isNaN(data)) {
        alert("숫자만 입력할 수 있습니다.");
        this.month = 1;
      }
    },
  },
  props: {
    roomData: Object,
    clicked: Number,
    hidden: Boolean,
    // 부모 컴포넌트에게서 받아온 데이터의 자료형 이름을 적어준다
    // 받아온 데이터의 값을 자식 컴포넌트가 재할당 할 수 없다. read-only
  },
};
</script>

<style>
.overlay {
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  position: fixed;
  backdrop-filter: blur(2px);
}

.modal {
  width: 500px;
  padding: 40px;
  margin: 40px auto;
  border-radius: 8px;
  background-color: #fff;
}
</style>
