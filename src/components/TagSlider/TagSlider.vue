<template>
  <div>
    <div class="tag-list d-flex flex-wrap mt-2">
      <div class="tag">
        Prada
      </div>
      <div class="tag">
        Prada
      </div>
      <div class="tag">
        Prada
      </div>
      <div class="tag">
        Prada
      </div>
      <div class="tag">
        Prada
      </div>
      <div class="tag">
        Prada
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data(){
    return {
      tags: []
    }
  },
}
</script>
<style>

.tag{
  color: #000000;
  background: #eee;
  display: inline-block;
  font-size: 13px;
  font-weight: bold;
  padding: 2px 7px;
  border-radius: 10px;
  margin-right: 5px;
  margin-bottom: 5px;
}
</style>