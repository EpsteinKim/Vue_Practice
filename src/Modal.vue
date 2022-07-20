<template>
  <div class="black-bg" v-show="modal.on">
    <div class="white-bg">
      <button class="close-modal" @click="closeModal">X</button>
      <h4>{{ modal.title }}</h4>
      <p>{{ modal.content }}</p>
      <img :src="modal.image" class="room-img" />
      <DiscountDiv />
    </div>
  </div>
</template>

<script>
// 데이터보내고 / 등록하고 / 쓰셈
export default {
  name: "ModalDiv",
  // props의 수신 컴포넌트는 받아올 데이터의 자료형 이름을 대문자로 작성 ( 디버그 용도 )
  props: {
    modal: Object,
    closeModal: function () {},
  },
};
</script>

<style></style>
