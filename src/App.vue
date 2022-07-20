<template>
  <div>
    <Modal :modal="modal" @closeModal="closeModal" />

    <div class="menu">
      <a v-for="(menu, index) in menus" :key="index">{{ menu }}</a>
    </div>

    <DiscountDiv />
    <div v-for="product in products" :key="product.id">
      <CardDiv @openModal="openModal(product.title, product.content, product.image)" :product="product" />
      <!-- custom event = @이름 : 이름이 수신되면 실행될 함수 -->
    </div>
  </div>
</template>

<script>
import data from "./assets/post.js";
import DiscountDiv from "./Discount.vue";
import Modal from "./Modal.vue";
import CardDiv from "./Card.vue";

export default {
  name: "App",
  data() {
    return {
      products: data,
      menus: ["Home", "Shop", "About"],
      singo: [0, 0, 0],
      modal: {
        on: false,
        title: "",
        content: "",
        image: "",
      },
    };
  },
  methods: {
    openModal(title, content, image) {
      this.modal.on = true;
      this.modal.title = title;
      this.modal.content = content;
      this.modal.image = image;
    },
    closeModal() {
      this.modal.on = false;
    },
  },
  components: {
    DiscountDiv,
    Modal,
    CardDiv,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

body {
  background-color: gray;
  margin: 0;
}

div {
  box-sizing: border-box;
}

.open-modal {
  cursor: pointer;
}

.open-modal:hover {
  transition: all ease 500ms;
  color: white;
}

.close-modal {
  position: absolute;
  right: 40px;
  top: 30px;
  border: none;
  cursor: pointer;
  height: 20px;
}

.black-bg {
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  position: fixed;
  padding: 20px;
}

.white-bg {
  width: 100%;
  background-color: white;
  border-radius: 8px;
  padding: 20px;
  z-index: 2;
}

.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}

.menu a {
  color: white;
  padding: 10px;
}

.room-img {
  width: 100%;
  margin-top: 40px;
}
</style>
