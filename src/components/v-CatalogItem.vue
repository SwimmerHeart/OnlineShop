<template>
  <v-card
      class="mx-auto my-12"
      :class="this.product_data.sold ? 'sold': ''"
      max-width="280px"
      height="328px"
      flat
      outlined
  >
    <v-img
        :src="require(`../assets/${product_data.image}`)"
        contain
        height="160"
    ></v-img>
    <v-hover v-slot="{ hover }">
      <h2 class="px-5 mt-5 card-title"
          :class="{ 'on-hover-title': hover }"
          @click.stop="openPopup"
      >{{ product_data.name }}
      </h2>
    </v-hover>
    <v-card-text
        class="d-flex align-center justify-space-between px-6"
        v-if="product_data.available"
    >
      <div>
        <div class="font-weight-light text-decoration-line-through price-prev"
             v-if="product_data.discount"
        >{{ formatedPrice(product_data.price) }} $
        </div>
        <div class="font-weight-bold price">{{ calculatePrice }} $</div>
      </div>
      <v-hover v-slot="{ hover }">
        <v-btn
            class="white--text font-weight-bold text-capitalize"
            depressed
            tile
            color="var(--btn-bg-ok)"
            width="118px"
            height="48px"
            :class="{ 'on-hover': hover, 'btn-loader': loading }"
            :loading="loading"
            :disabled="loading"
            @click="removeToCart"
            v-if="ToCart"
        >
          <svg-icon
              left
              type="mdi"
              :path="path"
              class="icon-button mr-1"
          >
          </svg-icon>
          В корзине
        </v-btn>
        <v-btn class="white--text font-weight-bold text-capitalize"
               depressed
               tile
               color="var(--btn-bg)"
               width="118px"
               height="48px"
               :class="{ 'on-hover': hover, 'btn-loader': loading }"
               :loading="loading"
               :disabled="loading"
               v-else
               @click="addToCart"
        >
          Купить
        </v-btn>
      </v-hover>
    </v-card-text>
    <v-card-text
        class="d-flex align-end justify-space-between"
        v-else>
      <div class="font-weight-bold sold-text pt-3">Продана на аукционе</div>
    </v-card-text>
    <v-row justify="center">

      <v-dialog
          v-model="dialog"
          max-width="700"
      >
        <v-card>
          <v-card-title class="text-h5">
            {{ product_data.name }}
          </v-card-title>

          <v-card-text>
            Lorem ipsum dolor sit amet, consectetur adipisicing elit. Animi architecto atque autem corporis cumque dolor
            error eveniet excepturi magnam, necessitatibus, odio optio pariatur quam, quisquam quod reprehenderit sint
            sunt totam?
          </v-card-text>
          <v-card-text class="text-center">
            <div class="d-flex align-center justify-center">
              <h3 class="text-h6 mr-5">Стоимость покупки: </h3>
              <div>
                <div class="font-weight-light text-decoration-line-through price-prev"
                     v-if="product_data.discount"
                >{{ formatedPrice(product_data.price) }} $
                </div>
                <div class="font-weight-bold price">{{ calculatePrice }} $</div>
              </div>
            </div>
          </v-card-text>
          <v-carousel hide-delimiter-background height="200">
            <v-carousel-item
                v-for="(image,i) in images"
                :key="i"
                :src="image.src"
                reverse-transition="fade-transition"
                transition="fade-transition"
            ></v-carousel-item>
          </v-carousel>

          <v-card-actions>
            <v-spacer></v-spacer>
            <v-hover v-slot="{ hover }">
              <v-btn
                  class="white--text font-weight-bold text-capitalize"
                  depressed
                  tile
                  color="var(--btn-bg-ok)"
                  width="118px"
                  height="48px"
                  :class="{ 'on-hover': hover, 'btn-loader': loading }"
                  :loading="loading"
                  :disabled="loading"
                  @click="removeToCart"
                  v-if="ToCart"
              >
                <svg-icon
                    left
                    type="mdi"
                    :path="path"
                    class="icon-button mr-1"
                >
                </svg-icon>
                В корзине
              </v-btn>
              <v-btn class="white--text font-weight-bold text-capitalize"
                     depressed
                     tile
                     color="var(--btn-bg)"
                     width="118px"
                     height="48px"
                     :class="{ 'on-hover': hover, 'btn-loader': loading }"
                     :loading="loading"
                     :disabled="loading"
                     v-else
                     @click="addToCart"
              >
                Купить
              </v-btn>
            </v-hover>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </v-row>
  </v-card>
</template>

<script>
import SvgIcon from '@jamescoyle/vue-icon';
import { mdiCheck } from '@mdi/js';

export default {
  name: "v-CatalogItem.vue",
  components: {
    SvgIcon
  },
  props: {
    product_data: {
      type: Object,
      default() {
        return {}
      }
    },
    cart:{
      type: Array,
      default() {
        return []
      }
    }
  },
  data: () => ({
    discountPrice: 0,
    oldPrice: '',
    dialog: false,
    images: [
      {
        src: 'https://cdn.vuetifyjs.com/images/carousel/squirrel.jpg',
      },
      {
        src: 'https://cdn.vuetifyjs.com/images/carousel/sky.jpg',
      },
      {
        src: 'https://cdn.vuetifyjs.com/images/carousel/bird.jpg',
      },
      {
        src: 'https://cdn.vuetifyjs.com/images/carousel/planet.jpg',
      },
    ],
    loader: null,
    loading: false,
    isToCart: false,
    path: mdiCheck
  }),
  methods: {
    formatedPrice(price) {
      this.oldPrice = price
      return this.oldPrice.toString().replace(/\B(?=(\d{3})+(?!\d))/g, " ")
    },
    openPopup() {
      this.dialog = true
    },
    addToCart() {
      this.dialog = false
      this.loader = 'loading'
      this.$emit('addToCart', this.product_data)
      setTimeout(() => {
        this.isToCart = !this.isToCart
      }, 2000)
    },
    removeToCart() {
      this.dialog = false
      this.loader = 'loading'
      this.$emit('removeToCart', this.product_data)
      setTimeout(() => {
        this.isToCart = !this.isToCart
      }, 2000)
    },
  },
  computed: {
    calculatePrice() {
      this.discountPrice = this.product_data.price - this.product_data.discount
      return this.discountPrice.toString().replace(/\B(?=(\d{3})+(?!\d))/g, " ")
    },
    ToCart(){
      this.cart.forEach(item=>{
        if(item.article === this.product_data.article){
          this.isToCart = true
        }
      })
      return this.isToCart
    }
  },
  watch: {
    loader () {
      const l = this.loader
      this[l] = !this[l]
      setTimeout(() => {
        this[l] = false
      }, 2000)
      this.loader = null
    },
  },
}
</script>

<style>
.card-title {
  font-size: 18px;
  font-weight: 400;
  line-height: 1.5;
}

.price-prev {
  font-size: 13px;
  color: #A0A0A0;
}

.price {
  color: #343030;
}
.on-hover-title{
  cursor: pointer;
}
.sold{
  opacity: .5;
}
.sold-text{
  font-size: 16px;
  line-height: 1.5;
  height: 48px;
}
.icon-button{
  width: 14px;
  height: 10px;
}
.btn-loading{
  background: var(--btn-bg-loading);
}
</style>