<template>
    <div>
        <text class="split" v-if="isSplit">{{label}}</text>
        <div class="wrapper" @click="onCellClicked" v-else>
            <slot name="icon">
                <image :src="icon" v-if="icon" class="icon"></image>
            </slot>
            <slot name="label">
                <text class="label" v-if="label">{{label}}</text>
            </slot>
            <image :src="arrowIcon"
                   class="cell-arrow-icon"
                   :aria-hidden="true"
                   v-if="hasArrow"></image>
        </div>
    </div>
</template>

<script>
    var navigator = weex.requireModule('navigator');
    export default {
        props: {
            icon: {
                type: String,
                default: ''
            },
            label: {
                type: String,
                default: ''
            },
            hasArrow: {
                type: Boolean,
                default: true
            },
            arrowIcon: {
                type: String,
                default: 'https://gw.alicdn.com/tfs/TB11zBUpwMPMeJjy1XbXXcwxVXa-22-22.png'
            },
            href: {
                type: String,
                default: ''
            },
            windowTitle: {
                type: String,
                default: ''
            },
            isSplit: {
                type: Boolean,
                default: false
            },
        },
        methods: {
            onCellClicked(event) {
                const href = this.href;
                const title = this.windowTitle;
                console.log("title " + title);
                if(href.length > 0) {
                    navigator.push({
                        page: href,
                        title: title
                    });
                }
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
        border-bottom-color: #e2e2e2;
        border-bottom-width: 1px;
        height: 100px;
    }
    .wrapper:active {
        background-color: #F2F2F2;
    }
    .label {
        flex: 1;
        font-size: 32px;
        color: black;
        text-align: left;
    }
    .icon {
        width: 32px;
        height: 32px;
        margin-right: 24px;
    }
    .cell-arrow-icon {
        width: 22px;
        height: 22px;
    }
    .split {
        background-color: #eee;
        font-size: 26px;
        height: 60px;
        padding-left: 24px;
        line-height: 60px;
        color: #999;
        border-bottom-color: #e2e2e2;
        border-bottom-width: 1px;
    }
</style>