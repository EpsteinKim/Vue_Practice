<template>
  <div class="black-bg" v-show="modal.on">
    <div class="white-bg">
      <button class="close-modal" @click="closeModal">X</button>
      <img :src="modal.image" class="room-img" />
      <h4>{{ modal.title }}</h4>
      <p>{{ modal.content }}</p>
      <input v-model="month" />
      <p>{{ month }}개월 선택함 : {{ modal.price * month }} 원</p>
    </div>
  </div>
</template>

<script>
// 데이터보내고 / 등록하고 / 쓰셈
export default {
  name: "ModalDiv",
  data() {
    return {
      month: 1,
    };
  },
  // props의 수신 컴포넌트는 받아올 데이터의 자료형 이름을 대문자로 작성 ( 디버그 용도 )

  beforeUpdate() {
    if (this.month == 2) {
      alert("2개월은 너무 적음 3개월 이상 하셈");
      this.month = 3;
    }
  },

  watch: {
    month(nextVal, curVal) {
      if (nextVal >= 13) {
        alert("13이상 입력하지 마셈");
        this.month = curVal;
      } else if (nextVal.match(/[^\d]/)) {
        alert("문자 넣지 마셈");
        this.month = curVal;
      }
    },
  },
  props: {
    modal: Object,
  },
  methods: {
    closeModal() {
      this.month = 1;
      this.$emit("closeModal");
    },
  },
};
</script>

<style></style>
