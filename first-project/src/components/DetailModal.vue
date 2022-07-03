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
      <p>{{ roomData[clicked].price }}만원</p>
      <!-- <button @click="hidden = false">닫기</button> -->
    </div>
  </aside>
</template>

<script>
export default {
  name: "DetailModal",
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
