<template>
  <v-footer color="var(--bg-footer)" class="d-flex justify-center flex-wrap">
      <div class="d-flex align-center flex-wrap justify-space-around align-center">
        <v-toolbar dense
                   flat
                   class="d-flex align-center justify-center"
                   color="var(--bg-footer)"
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
        <div class="d-flex">
          <div class="d-flex align-center flex-nowrap px-md-7 px-sm-4">
            <svg-icon type="mdi" :path="path1" class="icon-footer mr-2"></svg-icon>
            <div>+7 (812) 555-55-55</div>
          </div>
          <div class="d-flex align-center flex-nowrap px-md-7 px-sm-4">
            <svg-icon type="mdi" :path="path2" class="icon-footer mr-2"></svg-icon>
            <div>г. Санкт-Петербург, ул. Ефимова, 3</div>
          </div>
        </div>
      </div>
  </v-footer>
</template>

<script>
import SvgIcon from '@jamescoyle/vue-icon';
import { mdiPhone } from '@mdi/js';
import { mdiMapMarker } from '@mdi/js';
export default {
  name: "v-BlockFooter.vue",
  components:{
    SvgIcon
  },
  data() {
    return {
      path1: mdiPhone,
      path2: mdiMapMarker,
    }
  }
}
</script>

<style>
.icon-footer{
  width: 10px;
  height: 14px;
}
</style>