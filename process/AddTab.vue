<template>
  <div class="panel panel-primary">

    <div class="panel-heading apt-addheading"
      @click="hidepanel=!hidepanel">
      <span class="glyphicon glyphicon-plus"></span> Add Tab
    </div><!-- panel-heading -->

    <div class="panel-body"
      :class="{ hide: hidepanel }">

      <form class="add-tab form-horizontal"
        @submit.prevent="requestAdd">

        <div class="form-group" :class="titleEmpty ? 'has-error' : ''">
          <label class="col-sm-2 control-label" htmlFor="title">Title</label>
          <div class="col-sm-10">
            <input type="text" class="form-control" id="title" placeholder="Title" 
            ref="title"
            @blur="validate('title')"
            v-model="formData.title" />
          </div><!-- col-sm-10 --> 
        </div><!-- form-group --> 

        <div class="form-group" :class="serviceEmpty ? 'has-error' : ''">
          <label class="col-sm-2 control-label" htmlFor="service">Service</label>
          <div class="col-sm-10">
            <select class="form-control" id="service" placeholder="Service" 
              ref='service'
              @blur="validate('service')"
              v-model="formData.service" >
              <option>Service 1</option>
              <option>Service 2</option>
              <option>Service 3</option>
            </select>
          </div><!-- col-sm-10 -->
        </div><!-- form-group --> 

        <div class="form-group" :class="quantityEmpty ? 'has-error' : ''">
          <label class="col-sm-2 control-label" htmlFor="quantity">Quantity</label>
          <div class="col-sm-10">
            <input type="text" class="form-control"
              id="quantity" placeholder="Quantity" 
              ref='quantity'
              @blur="validate('quantity')"
              v-model="formData.quantity" />
          </div><!-- col-sm-10 -->
        </div><!-- form-group --> 

        <div class="form-group" :class="unitCostEmpty ? 'has-error' : ''">
          <label class="col-sm-2 control-label" htmlFor="unitCost">Unit Cost</label>
          <div class="col-sm-10">
            <input type="text" class="form-control"
              id="unitCost" placeholder="Unit Cost" 
              ref='unitCost'
              @blur="validate('unitCost')"
              v-model="formData.unitCost" />
          </div><!-- col-sm-10 -->
        </div><!-- form-group --> 

        <div class="form-group">
          <div class="col-sm-offset-2 col-sm-10">
            <button type="submit" class="btn btn-primary pull-right">Add Tab</button>
          </div><!-- col-sm-offset-2 --> 
        </div><!-- form-group -->

      </form>
    </div><!-- panel-body -->
  </div><!-- panel-primary -->
</template>

<script>

export default {

  name: 'AddTab',

  data() {
    return {
      hidepanel: true,
      formData: [],
      titleEmpty: true,
      serviceEmpty: true,
      quantityEmpty: true,
      unitCostEmpty: true,
    } //return
  }, //data
  
  methods: {
    requestAdd: function() {
      if(!this.titleEmpty && !this.serviceEmpty && !this.quantityEmpty && !this.unitCostEmpty){
        var parsedData = {
          title: this.formData.title,
          service: this.formData.service,
          quantity: this.formData.quantity,
          unitCost: this.formData.unitCost
        }
        this.$emit('addRecord', parsedData);
        this.formData = [];
        this.hidepanel = true;
        this.titleEmpty = true;
        this.serviceEmpty = true;
        this.quantityEmpty = true;
        this.unitCostEmpty = true;
      }
    }, //requestAdd

    validate: function(myRef) {
      if (this.$refs[myRef].value) {
        this._data[myRef + 'Empty'] = false;
      } else {
        this._data[myRef + 'Empty'] = true;
      }
    }
  }, //methods

} //default
</script>

<style scoped>

  .panel-heading {
    cursor: pointer;
  }

</style>
 