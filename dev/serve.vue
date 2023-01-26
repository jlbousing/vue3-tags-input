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
        {{ tagsSelect }}
        <vue3-tags-input v-model:tags="tagsSelect"
                         v-model="tag"
                         :select="true"
                         placeholder="multiple"
                         :select-items="suggestItems"
                         :duplicate-select-item="false"
                         @on-select="handleSelectedTag">
          <template #item="{ tag, index }">
            {{ tag.name }}
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
  computed: {
    // suggestions filtration for select modes
    suggestItems() {
      if (this.tag) {
        return this.selectItems.filter(e => e.name.toLowerCase().indexOf(this.tag.toLowerCase()) !== -1)
      } else {
        return this.selectItems
      }
    }
  },
  data() {
    return {
      tag: '',
      tags: ['VUE', 'HTML', 'CSS'],
      tagsSelect: [],
      selectItems: [
        { name: 'HTML', id: 1 },
        { name: 'CSS', id: 2 },
        { name: 'VUE', ida: 3 },
        { name: 'HTML1', id: 4 },
        { name: 'CSS1', id: 5 },
        { name: 'VUE1', id: 6 },
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
      this.tag = ''
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
