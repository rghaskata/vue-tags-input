<template>
  <div class="card">
    <div class="card-header">
      <h5>Products Tags Input</h5>
    </div>
    <div class="card-body">
      <div class="input-group gap-2">
        <input type="text" class="rounded form-control" v-model.trim="newTag" placeholder="Enter tags"
          @keypress.prevent.stop.enter="addTags" />
        <button type="button" class="rounded btn btn-sm btn-outline-dark" :disabled="!newTag"
          @click.prevent.stop="addTags"> Add
        </button>
        <button v-if="tagsList.length > 1" type="button" class="rounded btn btn-sm btn-outline-danger"
          @click.prevent.stop="clearTags"> Clear All
        </button>
      </div>
      <span v-if="tagExists" class="text-danger mb-2">Tag is already addded in list!!!</span>
      <div class="row">
        <div class="col-auto mt-3" v-for="(tag, index) in tagsList" :key="index">
          <div class="p-2 me-2 bg-primary text-white position-relative text-wrap text-start rounded">
            {{ tag.title }}
            <button class="btn btn-sm position-absolute top-0 start-100 translate-middle badge rounded-pill bg-danger"
              @click="removeTag(index)">
              &times;
            </button>
          </div>
        </div>
      </div>
    </div>
    <div class="card-footer">
      {{ tagsList }}
    </div>
  </div>
</template>
<script setup>
import { ref } from "vue";
const tagExists = ref(null);
const newTag = ref(null);
const selectedProduct = ref({
  id: 'YOUR_PRODUCT_ID',
  title: 'Amazing T-shirt'
});
const tagsList = ref([]);
const removeTag = (index) => {
  tagsList.value.splice(index, 1);
};
const clearTags = () => {
  newTag.value = "";
  tagExists.value = false;
  tagsList.value = [];
};
const addTags = () => {
  tagExists.value = false;
  tagsList.value.forEach((existingTag) => {
    if (existingTag.title === newTag.value) {
      tagExists.value = true;
    }
  });
  if (newTag.value && !tagExists.value) {
    tagsList.value.push({
      id: null,
      productId: selectedProduct.value.id,
      title: newTag.value,
    });
    newTag.value = "";
  }
};
</script>