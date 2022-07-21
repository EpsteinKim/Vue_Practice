<template>
  <div class="discount">
    <h4>지금 결제하면 {{ discountPer }}% 할인</h4>
  </div>
</template>

<script>
export default {
  name: "DiscountDiv",
  props: {
    discountPer: Number,
  },
};
</script>

<style scoped>
.discount {
  background: #eee;
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
}
</style>
