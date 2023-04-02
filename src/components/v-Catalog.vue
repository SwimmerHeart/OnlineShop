<template>
  <v-main class="main-block">
    <v-container class="content">
      <h1 class="main-title mt-8 px-3">Картины эпохи Возрождения</h1>
      <div class="d-flex justify-space-between align-start flex-wrap">
        <VCatalogItem v-for="product in products"
                      :key="product.article"
                      :product_data="product"
                      :cart="cartPicture"
                      @addToCart="addToCart"
                      @removeToCart="removeToCart"
        />
      </div>
    </v-container>
  </v-main>
</template>

<script>
import VCatalogItem from './v-CatalogItem';

export default {
  name: "Main-Block.vue",
  components: {VCatalogItem},
  props: {
    products: {
      type: Array,
      default() {
        return []
      }
    }
  },
  data() {
    return {
      cartPicture: []
    }
  },
  mounted() {
    if (localStorage.getItem('cartPicture')) {
      try {
        this.cartPicture = JSON.parse(localStorage.getItem('cartPicture'));
      } catch (e) {
        localStorage.removeItem('cartPicture');
      }
    }
  },
  methods: {
    addToCart(data) {
      //Добавляем в корзину
      const copyProduct = {...data, available: false}
      if (this.cartPicture.length) {
        if (this.cartPicture.findIndex(item => item.article === copyProduct.article) === -1) {
          this.cartPicture.push(copyProduct)
        }
      } else {
        this.cartPicture.push(copyProduct)
      }
      const parsed = JSON.stringify(this.cartPicture);
      localStorage.setItem('cartPicture', parsed);
    },
    removeToCart(data) {
      //Удаляем из корзины при повторном нажатии
      const copyProduct = {...data, available: true}
      if (localStorage.getItem('cartPicture')) {
        try {
          this.cartPicture = JSON.parse(localStorage.getItem('cartPicture'))
          this.cartPicture = this.cartPicture.filter(item => item.article !== copyProduct.article)
          const parsed = JSON.stringify(this.cartPicture);
          localStorage.setItem('cartPicture', parsed);
        } catch (e) {
          localStorage.removeItem('cartPicture');
        }
      }
    }
  }
}
</script>

<style>
.main-title {
  font-size: 24px;
  font-weight: 700;
}
.main-block{
  background: var(--main-bg);
}
</style>