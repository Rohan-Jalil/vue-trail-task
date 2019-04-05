<template>
  <li class="tab-item media">

    <div class="media-left">
      <button class="tab-delete btn btn-xs btn-success" title="Duplicate"
        @click="requestDuplicate">
      <span class="glyphicon glyphicon-plus"></span></button>
    </div><!-- media-left -->
    <div class="media-left">
      <button class="tab-delete btn btn-xs btn-danger" title="Delete"
        @click="requestRemoval">
      <span class="glyphicon glyphicon-remove"></span></button>
    </div><!-- media-left -->

    <div class="tab-info media-body">

      <div class="title-head">
        <span class="tab-title"
        >{{ tabTitle }}</span>
      </div><!-- tab-head -->

      <div class="service-name">
        <span class="label-item">Service:</span>
        <span
        >{{ tab.service }}</span>
      </div>
      <div class="quantity">
        <span class="label-item">Quantity:</span>
        <span
        >{{ tab.quantity }}</span>
      </div>
      <div class="cost">
        <span class="label-item">Cost:</span>
        <span
        >{{ tab.unitCost }}</span>
      </div>
      <div class="total-cost">
        <span class="label-item">Total Cost:</span>
        <span
        >{{ totalCost }}</span>
      </div>

    </div><!-- tab-info -->

  </li><!-- tab-item -->


</template>

<script>

import moment from 'moment';

export default {
  name: 'TabListItem',
  props: ['tab'],
  methods: {
    requestRemoval: function() {
      this.$parent.$emit('remove', this.tab);
    },
    requestDuplicate: function() {
      this.$parent.$emit('duplicate', this.tab);
    }

  }, //methods

  computed: {
    totalCost: function(){
      return this.tab.quantity * this.tab.unitCost;
    },

    tabTitle: function(){
      return this.tab.title + " " + this.totalCost;
    }
  },

} //default
</script>

<style scoped>

  .tab-item {
    border-bottom: 1px dotted gray;
    padding-bottom: 10px;
  }

  .tab-item:last-child {
    border-bottom: none;
  }

  .tab-title {
    font-weight: 600;
    color: #337ab7;
    font-size: 1.3em;
    line-height: 100%;
  }

  .tab-info {
    font-size: 1.7em;
  }

  .label-item {
    font-weight: 600;
    color: #667B82;
  }
  
  .tab-delete {
    font-size: 1.2em;
  }

  .apt-date {
    font-style: italic;
  }

  [contenteditable]:focus {
    outline: none;
    background: #EEE8D6; 
  }
</style>
