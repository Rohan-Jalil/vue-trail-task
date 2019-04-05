<template>
  <div id="main-app">
    <add-tab 
      @addRecord="addTab" />
    <tab-list
      :tabs = 'allTabs'
      @remove = 'removeItem'
      @duplicate = 'duplicateItem' />
  </div>
</template>

<script>

import _ from 'lodash';
import moment from 'moment';
import AddTab from './AddTab.vue';
import TabList from './TabList.vue';

export default {
  name: 'MainApp',
  data() {
    return {
      allTabs: []
    } //return
  }, //data

  components: {
    'add-tab': AddTab,
    'tab-list': TabList
  }, //components

  created: function() {
    $.getJSON('./builds/tabs.json')
      .done( info =>  {
        this.allTabs = info;
    }); //getJSON
  }, //created

  methods: {

    addTab: function(tab) {
      var newTab = _.clone(tab, true);
      this.allTabs.push(newTab);
    }, //addTab

    removeItem: function(tab) {
      this.allTabs = _.without(this.allTabs, tab);
    }, //removeItem
    
    duplicateItem: function(tab) {
      this.addTab(tab);
    }, //duplicateItem

  } //methods
} //default
</script>