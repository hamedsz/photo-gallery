<template>
  <div class="post pb-2">
    <div class="post__img-box">
      <img :src="img_url" :alt="title" class="post__img w-100">
      <div class="post__img-cover">
        <a :href="url">
          Open
        </a>
        <div class="post__domain">
          <LinkIcon class="mr-2" />
          {{ domain }}
        </div>
      </div>
    </div>

    <div class="tag-container">
      <div class="tag-list d-flex mt-2" :id="'tag_'+ id">
        <div class="tag" v-for="tag in listTags" :key="tag">
          {{ tag }}
        </div>
        <div class="left" @click="left">
          <ArrowLeftIcon />
        </div>
        <div class="right" @click="right">
          <ArrowRightIcon/>
        </div>
      </div>
    </div>

    <h6 class="post__title">
      {{ title }}
    </h6>
    <div class="post__description" v-html="description"></div>
  </div>
</template>
<script>
import LinkIcon from "@/components/Icon/LinkIcon";
import ArrowLeftIcon from "@/components/Icon/ArrowLeftIcon";
import ArrowRightIcon from "@/components/Icon/ArrowRightIcon";
export default {
  components: {ArrowRightIcon, ArrowLeftIcon, LinkIcon},
  props: {
    id: null,
    img_url: null,
    title: null,
    description: null,
    url: null,
    domain: null,
    tags: null,
  },
  computed: {
    listTags(){
      return this.tags.split(",")
    }
  },
  name: "PostItem",
  methods: {
    right(){
      console.log('here')
      let el = document.getElementById('tag_'+ this.id)

      el.scrollLeft += 100
    },
    left(){
      let el = document.getElementById('tag_'+ this.id)

      el.scrollLeft -= 100
    },
  }
}
</script>
<style lang="scss">
@import "post_item";
</style>