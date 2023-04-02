<template>
  <v-app>
      <VBlockHeader @searchProduct="searchProduct"/>
      <v-divider></v-divider>
      <VCatalog :products="filtered" />
      <VBlockFooter/>
  </v-app>
</template>

<script>
import VCatalog from './components/v-Catalog'
import VBlockFooter from './components/v-BlockFooter'
import VBlockHeader from './components/v-BlockHeader'

export default {
  name: 'App',

  components: {
    VBlockHeader,
    VBlockFooter,
    VCatalog
  },

  data: () => ({
    products:
      [
          {
            image: '1.jpg',
            name: '«Рождение Венеры» Сандро Боттичелли',
            price: 2000000,
            discount: 1000000,
            article: 1,
            available: true,
            sold: false
          },
        {
            image: '2.jpg',
            name: '«Тайная вечеря»  Леонардо да Винчи',
            price: 3000000,
            discount: 0,
            article: 2,
            available: true,
            sold: false
          },
        {
            image: '3.jpg',
            name: '«Сотворение Адама» Микеланджело',
            price: 6000000,
            discount: 1000000,
            article: 3,
            available: true,
            sold: false
          },
        {
            image: '4.jpg',
            name: '«Урок анатомии»  Рембрандт',
            price: 2000000,
            discount: 1000000,
            article: 4,
            available: false,
            sold: true
          },
      ],
    searchValue:'',

  }),
  methods:{
    searchProduct(value){
      this.searchValue = value
    }
  },
  computed:{
    filtered(){
      //Поиск по вводимым данным
      if(this.searchValue){
        return this.products.filter(item=> {
          return item.name.toLowerCase().includes(this.searchValue.toLowerCase())
        })
      }
      else {
        return this.products
      }
    }
  }

};
</script>

<style>
:root {
  --main-bg: #FFFFFF;
  --bg-footer: #ECEAEA;
  --main-color: #343030;
  --btn-bg: #403432;
  --btn-bg-hover: #776763;
  --btn-bg-ok: #5B3A32;
  --btn-bg-loading: #C1B4B1;
  --border: 1px solid #E1E1E1;
}


body{
  font-family: 'Merriweather', serif;
  background: #E5E5E5;
  color: var(--main-color);
}
* {
  padding: 0;
  margin: 0;
  list-style: none;
  outline: none;
  font-weight: 400;
  font-size: 14px;
  line-height: 1.5;
  box-sizing: border-box;
  font-family: 'Merriweather', serif;
}
a,
span,
p,
b,
h1,
h2,
h3,
h4,
h5 {
  color: var(--main-color);
}
a {
  text-decoration: none;
}

</style>
