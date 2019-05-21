<template>
  <div>
      <Header v-model="searchText"/>
      <div class="container">
        <div infinite-scroll-disabled="busy" infinite-scroll-distance="1000" v-infinite-scroll="loadMore"  class="row margin-bottom">
          <div v-for="(item,index) in list" :key="index" class="col-4">
            <div class="image-wrapper margin-bottom-md">
              <img :alt="item.user.name" class="responsive-image" :src="item.urls.small"/>
            </div>
            <h2 class="font-size-14 font-weight-7">{{item.user.name}}</h2>
          </div>
        </div>
      </div>
  </div>
</template>

<script>
import Header from './Header.vue'
import Unsplash, { toJson } from "unsplash-js";
const unsplash = new Unsplash({
  applicationId: "eeb89ad66933ae094352dcee4a037cc27ba514d19da2a3030a7eb15216d5d209",
  secret: "8c7b0acce7599f2d1aa9147dda3d352f6aaaa1c229a3c7c45c86566b6fb06316"
});
import infiniteScroll from 'vue-infinite-scroll';

export default {
  name: 'Home',
  components: {
    Header
  },
  directives: {infiniteScroll},
  props: {
  },
  data(){
    return{
        isLoading: true,
        ajaxPage: 1,
        list:[],
        search: false,
        hasMore: true,
        busy: false,
        searchText: ''
    }
  },
   created() {
  },
  methods: {
    loadMore(){
      this.busy = true;
        unsplash.photos.listPhotos(this.ajaxPage, 12, "latest")
        .then(toJson)
        .then(json => {
          this.busy = false;
          this.ajaxPage = this.ajaxPage+1
          this.list = this.list.concat(json);
        })
      }
  } 
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
