<template>
    <div class="wrapper" @click="onClicked">
        <slot name="label">
            <text class="label" v-if="label">{{label}}</text>
        </slot>
    </div>
</template>

<script>
    export default {
        props: {
            id: {
                type: String,
                default: ''
            },
            label: {
                type: String,
                default: ''
            }
        },
        methods: {
            onClicked(event) {
                const {id, label} = this;
                this.$emit('onBtnClicked', {event, id, label});
            }
        }
    }
</script>

<style scoped>
    .wrapper {
        flex-direction: row;
        align-items: center;
        padding-left: 24px;
        padding-right: 24px;
        background-color: #ffffff;
        border-color: #e2e2e2;
        border-width: 1px;
        height: 80px;
        border-radius: 12px;
    }
    .wrapper:active {
        background-color: #F2F2F2;
    }
    .label {
        flex: 1;
        font-size: 32px;
        color: #4f4f4f;
        text-align: center;
    }
</style>