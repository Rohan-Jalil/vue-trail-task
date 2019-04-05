<template>
  <ul class="tab-list">
    <tab-item 
      v-for="(item, i) in tabs"
      :tab="item"
      :key="i"
      :id="i"
    />
  </ul>
</template>

<script>

import TabListItem from './TabListItem.vue';

export default {
  name: 'TabList',

  props: ['tabs'],

  components: {
    'tab-item': TabListItem
  }, //components

} //export
</script>



<style scoped>
  .tab-list {
    margin: 0;
    padding: 0;
    list-style-type: none;
    margin: 10px 5%;
    font-size: 1rem;
  }
</style>