<!-- Inspired by bootstrap http://getbootstrap.com/ -->
<template>
  <div
    :class="['panel', 'panel-' + type]">
    <text
      :class="['panel-header', 'panel-header-' + type]">{{title}}</text>
    <div
      :class="['panel-body', 'panel-body-' + type]">
      <slot></slot>
    </div>
  </div>
</template>

<script>
  module.exports = {
    props: {
      type: { default: 'default' },
      title: { default: '' },
      dataClass: { default: '' },
    }
  }
</script>

<style scoped>
  .panel {
    background-color: #fff;
  }

  .panel-default {
  }

  .panel-primary {
    border-color: rgb(40, 96, 144);
  }

  .panel-success {
    border-color: rgb(76, 174, 76);

  }

  .panel-info {
    border-color: rgb(70, 184, 218);

  }

  .panel-warning {
    border-color: rgb(238, 162, 54);

  }

  .panel-danger {
    border-color: rgb(212, 63, 58);

  }

  .panel-header {
    background-color: #f5f5f5;
    font-size: 26px;
    padding-left: 24px;
    padding-right: 24px;
    padding-top: 20px;
    padding-bottom: 20px;
    color: #333;
  }

  .panel-header-default {
  }

  .panel-header-primary {
    background-color: #eee;
    color: #999;
  }

  .panel-header-success {
    background-color: rgb(92, 184, 92);
    color: #ffffff;
  }

  .panel-header-info {
    background-color: rgb(91, 192, 222);
    color: #ffffff;
  }

  .panel-header-warning {
    background-color: rgb(240, 173, 78);
    color: #ffffff;
  }

  .panel-header-danger {
    background-color: rgb(217, 83, 79);
    color: #ffffff;
  }

  .panel-header-tip {
    background-color: #fcf8e3;
    color: #8a6d3b;
    border-radius: 12px;
  }

  .panel-body {
    padding-left: 24px;
    padding-right: 24px;
    padding-top: 20px;
    padding-bottom: 20px;
  }

  .panel-body-default {
  }

  .panel-body-primary {
  }

  .panel-body-success {
  }

  .panel-body-info {
  }

  .panel-body-warning {
  }

  .panel-body-danger {
  }
</style>
