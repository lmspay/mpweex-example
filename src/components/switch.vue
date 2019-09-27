<template>
  <div>
    <div class="example">
      <text class="label">normal</text>
      <switch></switch>
    </div>
    <div class="example">
      <text class="label">checked</text>
      <switch checked="true"></switch>
    </div>
    <div class="example">
      <text class="label">disabled</text>
      <switch disabled="true" checked="true"></switch>
      <switch disabled="true" style="margin-left: 20px;"></switch>
    </div>
    <div class="example">
      <text class="label">onchange</text>
      <switch @change="onchange"></switch>
      <text class="info" style="margin-left: 20px;">{{checked}}</text>
    </div>
  </div>
</template>

<script>
    export default {
        data () {
            return {
                checked: false
            }
        },
        methods: {
            onchange (event) {
                console.log(`onchage, value: ${event.value}`)
                this.checked = event.value
            }
        }
    }
</script>

<style scoped>
  .example {
    flex-direction: row;
    justify-content: flex-start;
    align-items: center;
    margin-top: 60px;
  }
  .label {
    font-size: 40px;
    line-height: 60px;
    width: 200px;
    color: #666;
    text-align: left;
    margin-right: 20px;
    padding-left: 20px;
  }
  .info {
    font-size: 30px;
    line-height: 60px;
    color: #BBB;
    margin-left: 10px;
  }
</style>