<template>
    <div>
        <text class="split">scrollToElement</text>
        <scroller class="scroller">
            <div class="row" ref="item" v-for="(name, index) in rows" :key="index">
                <text class="text">{{name}}</text>
            </div>
        </scroller>
        <div class="btn-group">
            <text @click="goto(10)" class="button">Go to 10</text>
            <text @click="goto(20)" class="button">Go to 20</text>
        </div>

        <text class="split">getComponentRect</text>
        <div ref="box" class="box">
            <text class="info">Width: {{size.width}}</text>
            <text class="info">Height: {{size.height}}</text>
            <text class="info">Top: {{size.top}}</text>
            <text class="info">Bottom: {{size.bottom}}</text>
            <text class="info">Left: {{size.left}}</text>
            <text class="info">Right: {{size.right}}</text>
        </div>
    </div>
</template>


<script>
    const dom = weex.requireModule('dom')
    export default {
        data () {
            const rows = []
            for (let i = 0; i < 30; i++) {
                rows.push('row ' + i)
            }
            return {
                rows,
                size: {
                    width: 0,
                    height: 0,
                    top: 0,
                    bottom: 0,
                    left: 0,
                    right: 0
                }
            }
        },
        methods: {
            goto (index) {
                dom.scrollToElement(this.$refs.item[index], {})
            }
        },
        mounted () {
            setTimeout(() => {
                dom.getComponentRect(this.$refs.box, option => {
                if (option.result && option.size) {
                this.size = option.size
            }
        })
        }, 20);
        }
    }
</script>

<style scoped>
    .scroller {
        width: 700px;
        height: 300px;
        border-width: 3px;
        border-style: solid;
        border-color: rgb(162, 217, 192);
        margin-top: 20px;
        margin-left: 25px;
    }
    .split {
        background-color: #eee;
        font-size: 26px;
        height: 60px;
        padding-left: 40px;
        line-height: 60px;
        color: #666;
    }
    .row {
        height: 80px;
        justify-content: center;
        padding-left: 30px;
        border-bottom-width: 1px;
        border-bottom-style: solid;
        border-bottom-color: #DDDDDD;
    }
    .text {
        font-size: 32px;
        color: #666666;
    }
    .btn-group {
        flex-direction: row;
        justify-content: center;
        margin-top: 60px;
        margin-bottom: 60px;
    }
    .button {
        width: 200px;
        padding-top: 20px;
        padding-bottom: 20px;
        font-size: 40px;
        margin-left: 30px;
        margin-right: 30px;
        text-align: center;
        color: #41B883;
        border-width: 2px;
        border-style: solid;
        border-color: rgb(162, 217, 192);
        background-color: rgba(162, 217, 192, 0.2);
    }
    .box {
        width: 450px;
        height: 150px;
        background-color: #DDD;
        border-width: 2px;
        border-style: solid;
        align-self: center;
        margin-top: 60px;
        margin-bottom: 60px;
        border-color: rgb(162, 217, 192);
        background-color: rgba(162, 217, 192, 0.2);
    }
    .info {
        font-size: 16px;
    }
</style>