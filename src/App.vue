<template>
  <div>
    <transition name="fade">
      <Modal :modal="modal" @closeModal="closeModal" />
    </transition>

    <div class="menu">
      <a v-for="(menu, index) in menus" :key="index">{{ menu }}</a>
    </div>

    <DiscountDiv :discountPer="discountPer" />

    <button @click="priceLowSort">가격순 내림차순 정렬</button>
    <button @click="priceHighSort">가격순 오름차순 정렬</button>
    <button @click="nameSort">이름 순 정렬</button>
    <button @click="sortBack">되돌리기</button>

    <div v-for="product in products" :key="product.id">
      <CardDiv @openModal="openModal(product)" :product="product" />
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
      pureProducts: [...data],
      products: data,
      menus: ["Home", "Shop", "About"],
      singo: [0, 0, 0],
      modal: {
        on: false,
        title: "",
        content: "",
        image: "",
        price: "",
      },
      discountPer: 30,
    };
  },
  methods: {
    openModal(product) {
      const { title, content, image, price } = product;
      this.modal.on = true;
      this.modal.title = title;
      this.modal.content = content;
      this.modal.image = image;
      this.modal.price = price;
    },
    closeModal() {
      this.modal.on = false;
    },
    priceLowSort() {
      this.products.sort(function (a, b) {
        return a.price - b.price;
      });
    },
    priceHighSort() {
      this.products.sort((a, b) => b.price - a.price);
    },
    nameSort() {
      this.products.sort(function (a, b) {
        if (a.title > b.title) {
          return 1;
        }
        if (a.title < b.title) {
          return -1;
        }
        return 0;
      });
    },
    sortBack() {
      this.products = [...this.pureProducts];
    },
    percentageDownSec() {
      const temp = setInterval(() => {
        this.discountPer--;
        if (this.discountPer == 0) {
          clearInterval(temp);
        }
      }, 1000);
    },
  },
  mounted() {
    this.percentageDownSec();
  },
  components: {
    DiscountDiv,
    Modal,
    CardDiv,
  },
};
</script>

<style>
.fade-enter-from {
  opacity: 0;
}
.fade-enter-active {
  transition: all 500ms;
}
.fade-enter-to {
  opacity: 1;
}
.fade-leave-from {
  opacity: 1;
}
.fade-leave-active {
  transition: all 500ms;
}
.fade-leave-to {
  opacity: 0;
}

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
