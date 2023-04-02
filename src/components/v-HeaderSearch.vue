<template>
  <div class="d-flex align-center">
    <div>
      <input placeholder="Поиск по названию картины"
             class="search px-4"
             v-model="searchValue"
             @change="searchProduct"
      />
    </div>
    <div>
      <v-hover v-slot="{ hover }">
        <v-btn class="white--text font-weight-bold text-capitalize"
               depressed
               tile
               color="var(--btn-bg)"
               width="122px"
               height="48px"
               :class="{ 'on-hover': hover }"
        >
          Найти
        </v-btn>
      </v-hover>
    </div>
  </div>

</template>

<script>
export default {
  name: "Header-Search.vue",
  components: {},
  props:{
    product_data: {
      type: Array,
      default(){
        return []
      }
    }
  },
  data(){
    return{
      searchValue: ''
    }
  },
  methods:{
    searchProduct(){
      this.$emit('searchProduct', this.searchValue)
    }
  },
  watch:{
    searchValue(){
      this.searchProduct()
    }
  }
}
</script>

<style>
  .search{
    width: 250px;
    height: 48px;
    border: var(--border);
    background: var(--main-bg);
    color: var(--main-color);
    font-size: 14px;
    line-height: 1.5;
  }
  .on-hover{
    background: var(--btn-bg-hover)
  }
</style>