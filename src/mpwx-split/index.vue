<template>
    <div class="wrapper">
        <div class="line"></div>
        <text class="label">{{label}}</text>
        <div class="line"></div>
    </div>
</template>

<script>
    export default {
        props: {
            label: {
                type: String,
                default: ''
            }
        }
    }
</script>

<style scoped>
    .wrapper {
        flex-direction: row;
        justify-content: center;
        align-items: center;
    }
    .line {
        width: 120px;
        height: 1px;
        background-color: #CCCCCC;
    }
    .label {
        font-size: 24px;
        color: #999999;
        padding-left: 16px;
        padding-right: 16px;
    }
</style>