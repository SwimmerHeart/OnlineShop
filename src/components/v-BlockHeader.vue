<template>
    <v-app-bar
        class="header"
        flat
        color='var(--main-bg)'
        max-height="96px"
        height="96px"
    >
      <v-container class="content">
        <v-row align="center" class="d-flex">
          <v-col cols="6" md="7" sm="2">
            <v-app-bar-nav-icon v-if="$vuetify.breakpoint.mdAndDown"></v-app-bar-nav-icon>
            <v-toolbar dense
                       flat
                       class="d-flex align-center justify-center"
                       v-else
                       color='var(--main-bg)'
            >
              <v-btn
                  href="#"
                  text
                  small
              >
                <span class="text-capitalize">Каталог</span>
              </v-btn>
              <v-btn
                  href="#"
                  text
                  small
              >
                <span class="text-capitalize">Доставка</span>
              </v-btn>
              <v-btn
                  href="#"
                  text
                  small
              >
                <span class="text-capitalize">Оплата</span>
              </v-btn>
              <v-btn
                  href="#"
                  text
                  small
              >
                <span class="text-capitalize">Контакты</span>
              </v-btn>
              <v-btn
                  href="#"
                  text
                  small
              >
                <span class="text-capitalize">О компании</span>
              </v-btn>
            </v-toolbar>
          </v-col>
          <v-col cols="6" md="5" sm="10" class="d-flex align-center justify-end">
            <HeaderSearch @searchProduct="searchProduct" />
          </v-col>
        </v-row>
      </v-container>
    </v-app-bar>
</template>

<script>
import HeaderSearch from './v-HeaderSearch'

export default {
  name: "v-BlockHeader.vue",
  components:{
    HeaderSearch
  },
  methods:{
    searchProduct(value){
      this.$emit('searchProduct', value)
    }
  }
}
</script>

<style>
.header{
  border: var(--border);
}
.content{
  max-width: 1200px;
}
</style>