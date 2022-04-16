<template>
  <div id="app">
    <div class="container-fluid">
      <div class="search-box" v-bind:class="{focus: isSearchFocus}">
        <SearchIcon class="ml-3" />
        <input type="text" class="search-box__input" v-model="search" placeholder="Search for easy dinners, fashion, etc." @focus="isSearchFocus = true" v-on:blur="isSearchFocus = false">
      </div>

      <div class="row mt-5">
        <div class="col-xl-2 col-lg-2 col-md-4 col-sm-6 col-xs-6 col-x" v-for="i in columns" :key="i">
          <PostItem
              v-for="col in columnData(i-1)" :key="col.page_id"
              :img_url="col.image_url"
              :title="col.name"
              :description="col.description"
              :url="col.url"
              :domain="col.domain"
          />
        </div>
        <div class="d-flex justify-content-center p-3 w-100" v-if="search === ''">
          <div class="spinner-grow" role="status">
            <span class="sr-only">Loading...</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

import PostItem from "@/components/PostItem/PostItem";
import SearchIcon from "@/components/Icon/SearchIcon";

export default {
  name: 'App',
  data(){
    return {
      currentOffset: 0,
      columns: 6,
      data: [],
      search: "",
      isSearchFocus: false
    }
  },
  components: {
    SearchIcon,
    PostItem
  },
  computed: {
    dataPreview(){
      if (this.search !== ""){
        return this.data.filter(post => {
          let desc = post.description.toLowerCase()
          return desc.includes(this.search.toLowerCase())
        })
      }

      return this.data
    }
  },
  mounted() {
    this.getNextOffsetData()
    this.infintieScroll()
  },
  methods: {
    columnData(col){
      let items = [];

      for (var i=col; i < this.dataPreview.length; i += this.columns){
        items.push(this.dataPreview[i]);
      }

      return items
    },
    async infintieScroll(){
      window.onscroll = () => {
        let bottomOfWindow = document.documentElement.scrollTop + window.innerHeight === document.documentElement.offsetHeight;

        if (bottomOfWindow) {
          this.getNextOffsetData()
        }
      };
    },
    async getNextOffsetData(){
      let resp = await this.axios.get('http://xoosha.com/ws/1/test.php', {
        params: {
          offset: this.currentOffset
        }
      })

      this.data = this.data.concat(resp.data)
      this.currentOffset++;
    },
  }
}
</script>

<style lang="scss">
@import "app";
</style>
