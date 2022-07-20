<template>
  <div>
    <img :src="product.image" class="room-img" />
    <h4>
      <span class="open-modal" @click="$emit('openModal', product.title)">
        {{ product.title }}
      </span>
    </h4>
    <p>{{ product.price }}원</p>
  </div>
</template>

<script>
export default {
  name: "CardDiv",
  props: {
    product: Object,
  },
};
</script>

<style></style>
