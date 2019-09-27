<template>
  <div>
    <div style="padding: 30px;">
      <text style="font-size: 40px">oninput: {{txtInput}}</text>
      <text style="font-size: 40px">onchange: {{txtChange}}</text>
      <text style="font-size: 40px">onreturntype: {{txtReturnType}}</text>
      <text style="font-size: 40px">selection: {{txtSelection}}</text>
    </div>
    <scroller>
      <panel title="input type = text" type="primary">
        <input type="text" placeholder="Input Text" class="input" :autofocus=true value="" @change="onchange" @input="oninput"/>
      </panel>

      <panel title="input type = password" type="primary">
        <input type="password" placeholder="Input Password" class="input" @change="onchange" @input="oninput"/>
      </panel>

      <panel title="input type = url" type="primary">
        <input type="url" placeholder="Input URL" class="input" @change="onchange" @input="oninput"/>
      </panel>

      <panel title="input type = email" type="primary">
        <input type="email" placeholder="Input Email" class="input" @change="onchange" @input="oninput"/>
      </panel>

      <panel title="input type = tel" type="primary">
        <input type="tel" placeholder="Input Tel" class="input" @change="onchange" @input="oninput"/>
      </panel>

      <panel title="input type = time" type="primary">
        <input type="time" placeholder="Input Time" class="input" @change="onchange" @input="oninput"/>
      </panel>

      <panel title="input type = number" type="primary">
        <input type="number" placeholder="Input number" class="input" @change="onchange" @input="oninput"/>
      </panel>

      <panel title="input type = date" type="primary">
        <input type="date" placeholder="Input Date" class="input" @change="onchange" @input="oninput" max="2017-12-12" min="2015-01-01"/>
      </panel>

      <panel title="input return-key-type = default" type="primary">
        <input type="text" placeholder="please input" return-key-type="default" class="input" @change="onchange" @return = "onreturn" @input="oninput" />
      </panel>

      <panel title="input return-key-type = go" type="primary">
        <input type="text" placeholder="please input" return-key-type="go" class="input" @change="onchange" @return = "onreturn" @input="oninput" />
      </panel>

      <panel title="input return-key-type = next" type="primary">
        <input type="text" placeholder="please input" return-key-type="next" class="input" @change="onchange" @return = "onreturn" @input="oninput" />
      </panel>

      <panel title="input return-key-type = search" type="primary">
        <input type="text" placeholder="please input" return-key-type="search" class="input" @change="onchange" @return = "onreturn" @input="oninput" />
      </panel>

      <panel title="input return-key-type = send" type="primary">
        <input type="text" placeholder="please input" return-key-type="send" class="input" @change="onchange" @return = "onreturn" @input="oninput" />
      </panel>

      <panel title="input return-key-type = done" type="primary">
        <input type="text" placeholder="please input" return-key-type="done" class="input" @change="onchange" @return = "onreturn" @input="oninput" />
      </panel>

      <panel title="function focus() & blur()" type="primary">
        <div style="flex-direction: row;margin-bottom: 16px;justify-content: space-between">
          <text class="button" value="Focus" type="primary" @click="focus"></text>
          <text class="button" value="Blur" type="primary" @click="blur"></text>
        </div>

        <input type="text" placeholder="Input1" class="input" value="" ref="input1"/>
      </panel>

      <panel title="input selection" type="primary">
        <div style="flex-direction: row;margin-bottom: 16px;justify-content: space-between">
          <text class="button" value="setRange" type="primary" @click="setRange"></text>
          <text class="button" value="getSelectionRange" type="primary" @click="getSelectionRange"></text>
        </div>
        <input type="text"  ref="inputselection" placeholder="please input" value="123456789"  class="input" @change="onchange" @return = "onreturn" @input="oninput"/>
      </panel>

    </scroller>
  </div>
</template>

<style scoped>
  .input {
    font-size: 26px;
    height: 60px;
    line-height: 60px;
  }
  .button {
    font-size: 36;
    width: 200;
    color: #41B883;
    text-align: center;
    padding-top: 10;
    padding-bottom: 10;
    border-width: 2;
    border-style: solid;
    margin-right: 20;
    border-color: rgb(162, 217, 192);
    background-color: rgba(162, 217, 192, 0.2);
  }
</style>

<script>
  module.exports = {
    data: function () {
      return {
        txtInput: '',
        txtChange: '',
        txtReturnType: '',
        txtSelection:'',
        autofocus: false
      };
    },
      components: {
          panel: require('../include/panel.vue'),
      },
    methods: {
      ready: function () {
        var self = this;
        setTimeout(function () {
          self.autofocus = true;
        }, 1000);
      },
      onchange: function (event) {
        this.txtChange = event.value;
        console.log('onchange', event.value);
      },
      onreturn: function (event) {
        this.txtReturnType = event.returnKeyType;
        console.log('onreturn', event.type);
      },
      oninput: function (event) {
        this.txtInput = event.value;
        console.log('oninput', event.value);
      },
      focus: function () {
        this.$refs['input1'].focus();
      },
      blur: function () {
        this.$refs['input1'].blur();
      },
      setRange: function() {
        console.log(this.$refs["inputselection"]);
        this.$refs["inputselection"].setSelectionRange(2, 6);
      },
      getSelectionRange: function() {
        console.log(this.$refs["inputselection"]);
        var self = this;
        this.$refs["inputselection"].getSelectionRange(function(e) {
          self.txtSelection = e.selectionStart +'-' + e.selectionEnd;
        });
      }
    }
  };
</script>
