<template>
  <div>
    <div class="container">
      <div class="row">
        <div class="col-12">
          <div class="task">
            <h4 class="color" style="text-align: center; font-weight: bold">
              Detail
            </h4>
          </div>
        </div>
      </div>
    </div>
    <!-- <h1>this is number {{ productId }}</h1> -->
    <div class="detail">
      <div class="container">
        <div class="row">
          <div class="col-12 col-md-4">
            <img
              class="imgdt"
              :src="'http://apiecommerce.huesoft.net' + product.image_source"
              alt=""
            />
          </div>
          <div class="col-12 col-md-1 endbor"></div>
          <div class="col-12 col-md-7 bor">
            <h3 class="namepr">{{ product.title }}</h3>
            <h5 style="font-weight: bold; color: #f6a225; text-align: center">
              -- Giá: {{ product.price }}$ --
            </h5>
            <li>Content: {{ product.content }}</li>
            <!-- <button @click="clickhere">cilck to get product</button> -->
            <button class="btn btn-info float-right" @click="addToCart(product)">Add to Cart</button>
            <!-- <button @click="clickhere">cilck to get product</button>
            <router-link
              :to="'/detailproduct/' + 4"
              class="text-decoration-none"
              >click de thay doi san pham</router-link
            > -->
          </div>
        </div>
      </div>
    </div>
    <div class="container pt-5 mt-5">
      <div class="row mb-5">
        <h2 class="text-center w-100 custom_related">Product related</h2>
        <!-- <button @click="clickhere">clickhear</button> -->
      </div>
      <div class="row">
        <div class="col-md-12 custom_img">
          <VueSlickCarousel v-bind="settings">
            <div v-for="item in product.related.slice(0, 4)" :key="item.id">
              <div class="card mr-2">
                <div class="card-title text-center">{{ item.title }}</div>
                <div class="card-body">
                  <img
                    :src="'http://apiecommerce.huesoft.net' + item.image_source"
                    alt=""
                  />
                  <p class="text-center">Price: {{ item.price }}$</p>
                  <h4 class="mt-3 mb-2">
                    <!-- <router-link
                      class="w-100 text-center"
                      to=""
                      v-on:click="detailproduct()"
                      >{{ item.title }}</router-link
                    > -->
                    <button class="w-100">
                      {{ item.title }}
                    </button>
                  </h4>
                </div>
              </div>
            </div>
          </VueSlickCarousel>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import VueSlickCarousel from "vue-slick-carousel";
import "vue-slick-carousel/dist/vue-slick-carousel.css";
// optional style for arrows & dots
import "vue-slick-carousel/dist/vue-slick-carousel-theme.css";
export default {
  data() {
    return {
      nameproduct: null,
      product: [],
      productId: this.$route.params.id,
      settings: {
        arrows: true,
        dots: true,
        focusOnSelect: false,
        infinite: true,
        speed: 500,
        slidesToShow: 4,
        slidesToScroll: 1,
        touchThreshold: 5,
      },
    };
  },
  methods: {
    detailproduct() {
      this.nameproduct = "dinh hop";
      console.log(this.nameproduct);
    },
    addToCart(item) {
      this.$store.commit("addToCart", item);
    },
    // clickhere() {
    //   console.log(this.product);
    // },
  },
  mounted() {
    axios
      .get(
        "http://apiecommerce.huesoft.net/api/products/get?id=" + this.productId
      )
      .then((response) => (this.product = response.data.data))
      .catch((error) => console.log(error));
  },
  components: { VueSlickCarousel },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.custom_img img {
  width: 236px;
  height: 236px;
}
.custom_img .slick-next::before,
.custom_img .slick-prev::before {
  font-size: 40px;
  background: black;
}
.custom_img .slick-prev {
  left: -40px;
}
.custom_img .slick-next {
  right: 21px;
}
/* table, tr, td{
   border: 1px solid black;
   border-collapse: collapse;
} */
.help-block {
  color: red;
}

.left {
  display: flex;
  justify-content: flex-end;
}

.label {
  margin-bottom: 6px;
}

/* td {
   width: 160px;
   text-align: center;
} */
.custom_related {
  font-size: 40px;
}
.margin {
  margin: 5% 0% 0% 2%;
}

.margin-left {
  margin-left: 10%;
}

.mg {
  margin-left: 10%;
}

.bg-gradient-primary {
  background-image: linear-gradient(180deg, #374c8a 10%, #36b9cc 100%);
}

.mg-l {
  margin-left: 18%;
}

.mg-t {
  margin: 5% 0 0 1%;
}

.red {
  color: red;
}

.form-d {
  display: block;
  width: 100%;
  height: calc(1.5em + 0.75rem + 2px);
  padding: 0.375rem 0.75rem;
  font-size: 1rem;
  font-weight: 400;
  line-height: 1.5;
  color: #6e707e;
  background-color: #fff;
  background-clip: padding-box;
  border: 1px solid #d1d3e2;
  border-radius: 0.35rem;
  transition: border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
}
.top {
  position: relative;
  top: 30%;
}

.bg {
  background-color: #4e73df;
  background-image: linear-gradient(180deg, #1572a9 10%, #2b739b 100%);
  /* background-image: linear-gradient(180deg, #4e73df 10%, #224abe 100%); */
  background-size: cover;
  background-position: center;
}

.button {
  font-size: 0.8rem;
  border-radius: 10rem;
  padding: 0.75rem 1rem;
  color: #fff;
  background-color: #139cbc;
  border-color: #fff;
  display: block;
  width: 100%;
  border-bottom: none;
  border-right: none;
}

.button:focus {
  border: none;
  outline: none !important;
}

.form-center {
  margin: 0;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

a:hover {
  text-decoration: none;
}

.nav-item {
  font-weight: 600;
}

.tagp {
  font-size: 2rem;
  color: #fff;
  background: #767676;
  opacity: 0.6;
  /* border-radius: 50%;/ */
}

.tagh1 {
  font-size: 3rem;
  color: #fff;
  font-weight: 700;
  /* background: cadetblue; */
  background-color: #139cbc;
  border-radius: 50%;
  opacity: 0.8;
}

.widget-title {
  color: #0c9ee4;
  font-size: 22px;
  font-weight: 600;
  margin: 0;
  position: relative;
  text-align: center;
  z-index: 1;
}

.widget-title span {
  background: #fff none repeat scroll 0 0;
  padding: 0 15px;
}

.widget-title::after {
  background: #ddd none repeat scroll 0 0;
  bottom: 0;
  content: "";
  height: 1px;
  left: 0;
  margin: auto;
  position: absolute;
  right: 0;
  top: 0;
  z-index: -1;
}

.ten {
  color: darkslategray;
  margin-top: 1rem;
  font-weight: bold;
}

.ahover:hover {
  /* -webkit-box-shadow: 0 0 20px rgba(0, 0, 0, .1);
   box-shadow: 0 0 20px rgba(0, 0, 0, .1); */
  -webkit-box-shadow: 0 2px 40px 8px rgba(15, 15, 15, 0.15);
  box-shadow: 0 2px 40px 8px rgba(15, 15, 15, 0.15);
  z-index: 1;
  border-radius: 2%;
}

.price {
  color: #ff2d2d;
  font-weight: bold;
}

b {
  color: #4e73df;
}

.mt {
  margin-top: 21px;
}

.single-footer-widget .social-info a.facebook {
  background-color: #4b62b3;
}

.single-footer-widget .social-info a {
  display: inline-block;
  font-size: 17px;
  color: #ffffff;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  /* margin-right: 10px; */
  text-align: center;
}

.a {
  line-height: 40px;
}

.single-footer-widget .social-info a.twitter {
  background-color: #03baeb;
}

.single-footer-widget .social-info a.google-plus {
  background-color: #cb242e;
}

.single-footer-widget .social-info a.instagram {
  background-color: #057ad7;
}

.mb-30 {
  margin-bottom: 30px;
}

p {
  color: #6e6e6e;
}

.widget-titlee {
  margin-top: 20px;
  margin-bottom: 15px;
}

.padding-80-0 {
  padding-top: 50px;
  padding-bottom: 60px;
}

.footer-area {
  background: white;
}

.task {
  padding: 10px 10px 10px 10px;
  background: #f4f4f4 none repeat scroll 0 0;
  border: 1px solid #ddd;
  margin-top: 20px;
  margin-bottom: 30px;
}
.task > h4 {
  color: #f6a225;
  font-size: 1.5rem;
}
.imgdt {
  height: 390px;
  width: 390px;
  padding: 10px 0px;
  border-bottom: 1px solid;
  border-left: 1px solid;
  border-top: 1px solid;
  border-radius: 1%;
  color: black;
}

.endbor {
  /* border-right: 1px solid #d4caca;
   border-radius: 50%; */
  margin-left: -33px;
}

.bor {
  border-right: 1px solid black;
  margin-left: 22px;
  border-radius: 2%;
}

.namepr {
  font-weight: bold;
  margin-bottom: 1rem;
  font-size: 2rem !important;
  color: #63b4d5;
  text-align: center;
}

.ipwid {
  width: 5rem;
  text-align: center;
  background-clip: padding-box;
  border: 1px solid #ced4da;
  border-radius: 0.25rem;
  padding: 0.375rem 0.75rem;
  font-size: 1rem;
  line-height: 1.5;
  color: #495057;
  background-color: #fff;
  margin-right: 0.5em;
}

.quantity {
  margin-top: 21px;
}

.count {
  border: 1px solid;
  border-radius: 5px;
  padding: 3px;
  margin-top: 5px;
}

.padding-80 {
  padding-top: 80px;
  padding-bottom: 80px;
}

.bg-gray {
  background-color: #f6f9f9 !important;
}

.nam-cta-area .cta-thumbnail {
  position: absolute;
  height: 100%;
  z-index: -1;
  top: 0;
  right: 0;
}

.nam-cta-area .cta-content h2 {
  display: block;
  margin-bottom: 30px;
}

.nam-btn.active {
  border-color: #bca858;
  background-color: #bca858;
  color: #ffffff;
}

.nam-btn {
  font-family: "Playfair Display", serif;
  position: relative;
  z-index: 1;
  min-width: 150px;
  height: 42px;
  line-height: 40px;
  font-size: 14px;
  font-weight: 400;
  display: inline-block;
  padding: 0 35px;
  text-align: center;
  text-transform: uppercase;
  background-color: transparent;
  color: #252525;
  border: 1px solid #252525;
  border-radius: 60px;
}

.nam-btn:hover {
  border-color: #bca858;
  background-color: #bca858;
  color: #ffffff;
}

.nam-btn.active:focus,
.nam-btn.active:hover {
  border-color: #252525;
  background-color: #252525;
  color: #ffffff;
  box-shadow: 0 2px 40px 8px rgba(15, 15, 15, 0.15);
}

.pd-lr {
  padding: 0px 5px;
}

.mg-top {
  margin-top: 73px;
}

.total {
  margin-top: 53px;
  background: #f8f9fc;
}

.cart-left {
  padding: 17px 20px;
}

.cart-bott {
  padding: 17px 20px;
}

li {
  color: black;
}

.dathang {
  color: darkslategray;
  font-weight: 700;
  text-align: center;
  padding: 28px;
}

.bg-dh {
  background-color: #e5ebf1;
}
</style>
