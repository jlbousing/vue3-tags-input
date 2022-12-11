<template>
  <div id="app">
    <div class="form">
      <!--      npm publish-->
      <vue3-tags-input placeholder="add tags"
                       :tags="tags"
                       :validate="csValidate"
                       @on-focus="handleFocus"
                       @on-blur="handleBlur"
                       @on-remove="handleRemove"
                       @on-tags-changed="handleChangeTag">
        <template #item="{ name, index }">
          {{ name }}
        </template>
      </vue3-tags-input>
      <br>
      <div class="custom-input-tags">
        <vue3-tags-input v-model:tags="tagsSelect"
                         v-model="tag"
                         :select="true"
                         multiple
                         :select-items="selectItems"
                         @on-select="handleSelectedTag">
          <template #item="{ tag, index }">
            {{ tag.name }} {{ tag._key }}
          </template>
          <template #no-data>
            No Data
          </template>
          <template #select-item="tag">
            {{ tag.name }}
          </template>
        </vue3-tags-input>
        <input type="text" v-model="tag">
      </div>
    </div>
  </div>
</template>

<script>
import { defineComponent } from 'vue';
import Vue3TagsInput from '@/vue3-tags-input.vue';

export default defineComponent({
  name: 'ServeDev',
  components: {
    Vue3TagsInput
  },
  data() {
    return {
      tag: '',
      tags: ['VUE', 'HTML', 'CSS'],
      tagsSelect: [],
      selectItems: [
        { name: 'HTML', id1: 1 },
        { name: 'CSS', id1: 2 },
        { name: 'VUE', id1: 3 },
        { name: 'HTML1', id1: 4 },
        { name: 'CSS1', id1: 5 },
        { name: 'VUE1', id1: 6 },
      ]
    }
  },
  methods: {
    handleChangeTag(tags) {
      this.tags = tags;
    },
    csValidate(value) {
      const regex = new RegExp(/^[a-zA-Z]+$/);
      return regex.test(value)
    },
    handleSelectedTag(tag) {
      this.tagsSelect.push(tag)
    },
    handleFocus(event) {
      console.log('focus', event)
    },
    handleBlur(event) {
      console.log('blur', event)
    },
    handleRemove(index) {
      console.log('on remove', index)
    },
  }
});
</script>

<style>
body {
  font-family: Inter var,ui-sans-serif,system-ui,-apple-system,BlinkMacSystemFont,Segoe UI,Roboto,Helvetica Neue,Arial,Noto Sans,sans-serif,Apple Color Emoji,Segoe UI Emoji,Segoe UI Symbol,Noto Color Emoji;
}
.form {
  width: 300px;
}
</style>
