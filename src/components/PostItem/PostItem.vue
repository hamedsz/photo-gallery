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

    <h6 class="post__title">
      {{ title }}
    </h6>
    <div class="post__description" v-html="description"></div>
  </div>
</template>
<script>
import LinkIcon from "@/components/Icon/LinkIcon";
export default {
  components: {LinkIcon},
  props: {
    img_url: null,
    title: null,
    description: null,
    url: null,
    domain: null,
  },
  name: "PostItem",
  methods: {
  }
}
</script>
<style lang="scss">
@import "post_item";
</style>