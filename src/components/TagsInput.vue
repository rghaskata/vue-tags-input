<template>
  <div class="">
    <div class="input-group gap-2">
      <input type="text" class="rounded form-control" v-model.trim="newTag" placeholder="Enter tags"
        @keypress.prevent.stop.enter="addTags" />
      <button type="button" class="rounded btn btn-sm btn-outline-dark" :disabled="!newTag"
        @click.prevent.stop="addTags"> Add
      </button>
    </div>
    <span v-if="tagExists" class="text-danger">Tag is already addded in list!!!</span>
    <div class="row mt-4">
      <div class="col-auto mb-3" v-for="(tag, index) in tagsList" :key="index">
        <div class="p-2 me-2 bg-primary text-white position-relative text-wrap text-start rounded">
          {{ tag }}
          <button class="btn btn-sm position-absolute top-0 start-100 translate-middle badge rounded-pill bg-danger"
            @click="removeTag(index)">
            &times;
          </button>
        </div>
      </div>
    </div>
    {{ tagsList }}
  </div>
</template>
<script setup>
import { ref } from "vue";
const tagExists = ref(null);
const newTag = ref(null);
const tagsList = ref([]);
const removeTag = (index) => {
  tagsList.value.splice(index, 1);
};
const addTags = () => {
  tagExists.value = false;
  tagsList.value.forEach((existingTag) => {
    if (existingTag === newTag.value) {
      tagExists.value = true;
    }
  });
  if (newTag.value && !tagExists.value) {
    tagsList.value.push(newTag.value);
    newTag.value = "";
  }
};
</script>