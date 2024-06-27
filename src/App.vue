<script setup>
import HelloWorld from './components/HelloWorld.vue'
import TagsInput from './components/TagsInput.vue'
import ProductTagsInput from './components/ProductTagsInput.vue'
</script>

<template>
  <div class="container my-5">
    <div class="d-flex align-items-center justify-content-center gap-3">
      <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />
      <div class="wrapper">
        <HelloWorld msg="Vue3 Tags Input" />
      </div>
    </div>
    <div class="row">
      <div class="col-md-6 mb-3">
        <TagsInput />
      </div>
      <div class="col-md-6 mb-3">
        <ProductTagsInput />
      </div>
    </div>
  </div>
</template>