<template>
  <div>
    <div v-if="productReady" class="product-wrapper">
      <div class="product-image">
        <img :src="product.image" :alt="product.title" />
      </div>
      <div class="product-information" :key="product.id">
        <h1 class="product-title">
          {{ product.title }}
        </h1>
        <div class="rating-wrapper">
          <p class="product-category">{{ product.category }}</p>
          <p class="product-rating">
            {{ product.rating.rate }} / {{ product.rating.count }}
          </p>
        </div>
        <p class="product-description">{{ product.description }}</p>
        <div class="price-wrapper">
          <h2 class="product-price">${{ product.price }}</h2>
        </div>
        <div class="btn-wrapper">
          <button class="btn-buy">Buy Now</button>
          <button class="btn-next" v-on:click="changeToNextProduct">
            Next Product
          </button>
        </div>
      </div>
    </div>
    <div v-else-if="product" class="error-page">
      <div class="error-wrapper">
        <p>This product is unavailable to show</p>
        <button class="btn-next" v-on:click="changeToNextProduct">
          Next Product
        </button>
      </div>
      <div class="bg-error"></div>
    </div>
    <div v-else class="loader"></div>
    <!-- <div class="splash-bg"></div> -->
    <div class="bg-color" :class="BackgroundColor"></div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "ProductDisplay",
  data() {
    return {
      productReady: false,
      product: {},
      productIndex: 1,
      productCategory: "",
    };
  },
  methods: {
    changeToNextProduct() {
      this.productReady = false;
      this.product = {};
      if (this.productIndex < 20) {
        this.productIndex += 1;
      } else {
        this.productIndex = 1;
      }

      axios
        .get(`https://fakestoreapi.com/products/${this.productIndex}`)
        .then((res) => {
          this.product = res.data;
          this.productReady = true;
          if (this.product.category === "men's clothing") {
            this.productCategory = "men";
          } else if (this.product.category === "women's clothing") {
            this.productCategory = "women";
          } else {
            return "";
          }
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
  mounted() {
    this.productReady = false;
    this.product = {};
    axios
      .get(`https://fakestoreapi.com/products/21`)
      .then((res) => {
        this.product = res.data;
        this.productReady = true;

        if (this.product.category === "men's clothing") {
          this.productCategory = "men";
        } else if (this.product.category === "women's clothing") {
          this.productCategory = "women";
        } else {
          return "";
        }
      })
      .catch((error) => {
        console.log(error);
      });
  },
  computed: {
    BackgroundColor() {
      return {
        "men-bg-color": this.productCategory === "men",
        "women-bg-color": this.productCategory === "women",
      };
    },
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Inter:wght@100;200;300;400;500;600;700;800;900&display=swap");

.loader {
  border: 16px solid #f3f3f3; /* Light grey */
  border-top: 16px solid #6dbff5; /* Blue */
  border-radius: 50%;
  width: 120px;
  height: 120px;
  animation: spin 2s linear infinite;
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

.product-wrapper {
  display: flex;
  padding: 1.5em;
  width: 1034px;
  height: 580px;
  background: #ffffff;
  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
  border-radius: 10px;
}

.product-image {
  display: flex;
  align-items: center;
  justify-content: center;
}

.product-image img {
  object-fit: contain;
  width: 300px;
  height: 400px;
}
.product-information {
  display: flex;
  flex-direction: column;
  padding: 2em;
}

.product-title {
  color: #720060;
  text-align: left;
  margin-bottom: 0em;
}
.rating-wrapper {
  display: flex;
  border-bottom: 2px solid #cecece;
  padding: 1em 0em;
}
.product-category {
  flex-grow: 1;
  text-align: left;
}
.product-description {
  width: 517px;
  height: 163px;
  text-align: left;
  flex-grow: 1;
  padding: 1em 0em;
  width: 100%;

  font-family: "Inter";
  font-style: normal;
  font-weight: 400;
  font-size: 20px;
  line-height: 24px;

  border-bottom: 2px solid #cecece;
  color: #1e1e1e;
}

.product-price {
  text-align: left;
  padding: 0.5em 0em;
  font-family: "Inter";
  font-style: normal;
  font-weight: 600;
  font-size: 28px;
  line-height: 34px;
}

.btn-wrapper {
  display: flex;
  justify-content: center;
  gap: 1em;
}
.btn-buy {
  flex-grow: 1;
  height: 42px;

  color: white;
  background: #720060;
  border-radius: 4px;
}
.btn-next {
  flex-grow: 1;
  height: 42px;

  background: #ffffff;
  border: 3px solid #720060;
  border-radius: 4px;
  font-family: "Inter";
  font-style: normal;
  font-weight: 600;
  font-size: 20px;
  line-height: 24px;
}
.btn-next:hover {
  background-color: #e48cd7d7;
}

.bg-color {
  position: absolute;
  z-index: -1;
  left: -3px;
  top: 0px;
  width: 100vw;
  height: 550px;
}
.women-bg-color {
  background-color: #fde2ff;
}
.men-bg-color {
  background-color: #d6e6ff;
}

.error-page {
  display: flex;
  justify-content: center;
  align-items: center;

  width: 100vw;
  height: 40vh;
}
.bg-error {
  position: absolute;
  z-index: -1;
  left: -3px;
  top: 0px;
  width: 100vw;
  height: 550px;
  background-color: #d8d7d7;
}

.error-wrapper {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 2em;
  width: 1000px;
  height: 580px;
  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
  border-radius: 10px;
  background-color: white;
  background-image: url("../assets/sad-face.svg");
  background-repeat: no-repeat;
  background-position-x: -200%;
  background-position-y: center;
}
.error-wrapper p {
  font-family: "Inter";
  font-style: normal;
  font-weight: 400;
  font-size: 20px;
  line-height: 24px;
  margin-bottom: 1em;
}
.error-wrapper button {
  width: 50%;
  flex-grow: 0;
}
</style>