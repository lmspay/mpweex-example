<template>
  <scroller>
    <panel title="textarea" type="primary">
      <textarea
        class="textarea"
        autofocus="true"
        return-key-type="done"
        @return="onreturn"
        @change="onchange"
        @input="oninput"
      />
      <text class="tip">oninput: {{txtInput}}</text>
      <text class="tip">onchange: {{txtChange}}</text>
      <text class="tip">enter key type: {{returnType}}</text>
      <text class="tip">action: {{msg}}</text>
    </panel>
  </scroller>
</template>

<style scoped>
  .textarea {
    font-size: 32px;
    height: 280px;
    width: 400px;
    border-width: 2px;
    border-color: #ccc;
  }
  .tip {
    font-size: 32px;
    margin-top: 20px;
  }
</style>

<script>
  var modal = weex.requireModule('modal')
  module.exports = {
    data: function () {
      return {
        txtInput: '',
        txtChange: '',
        returnType: '',
        msg: ''
      }
    },
    components: {
      panel: require('../include/panel.vue')
    },
    methods: {
      onchange: function(event) {
        this.txtChange = event.value;
      },
      oninput: function(event) {
        this.txtInput = event.value;
      },
      onreturn: function(event) {
        this.returnType = event.returnKeyType;
        this.msg = 'You are "' + this.returnType + '" ' + event.value;
      }
    }
  };
</script>
