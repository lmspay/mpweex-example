<template>
    <div class="wrapper">
        <div></div>
        <div></div>
        <div class="root">
            <image :src="logo" class="logo"/>
            <text class="greeting">欢迎使用众圈小程序</text>

            <div class="index_btn_root" style="margin-top: 60px">
                <div class="index_btn_group" @click="jumpDefaultComponents">
                    <image class="index_btn_icon" src="mpweex://images/defcoms.png"></image>
                    <text class="index_btn_label">基础组件</text>
                </div>
                <div class="index_btn_group" style="margin-left: 24px" @click="jumpDefaultModules">
                    <image class="index_btn_icon" src="mpweex://images/defmods.png"></image>
                    <text class="index_btn_label">基础模块</text>
                </div>
            </div>
            <div class="index_btn_root" style="margin-top: 24px;" @click="jumpSeniorCM">
                <div class="index_btn_group">
                    <image class="index_btn_icon" src="mpweex://images/seniorcms.png"></image>
                    <text class="index_btn_label">高级组件、模块</text>
                </div>
                <div class="index_btn_group" style="margin-left: 24px" @click="jumpDemos">
                    <image class="index_btn_icon" src="mpweex://images/demos.png"></image>
                    <text class="index_btn_label">组件、模块案例</text>
                </div>
            </div>
        </div>
        <div></div>
    </div>
</template>

<script>
    var navigator = weex.requireModule('navigator');
    export default {
        name: 'App',
        data() {
            return {
                logo: 'mpweex://images/logo.png'
            }
        },
        methods: {
            jumpDefaultComponents(event) {
                navigator.push({
                    page: '/defcoms.js',
                    title: "基础组件"
                });
            },
            jumpDefaultModules(event) {
                navigator.push({
                    page: '/defmods.js',
                    title: "基础模块"
                });
            },
            jumpSeniorCM(event) {
                navigator.push({
                    page: '/seniorcms.js',
                    title: "高级组件、模块"
                });
            },
            jumpDemos(event) {
                navigator.push({
                    page: '/demos.js',
                    title: "组件、模块案例"
                });
            }
        }
    };
</script>

<style scoped>
    .wrapper {
        justify-content: space-between;
        background-color: white;
    }

    .root {
        align-items: center;
    }

    .logo {
        width: 200px;
        height: 200px;
    }

    .index_btn_icon {
        width: 100px;
        height: 100px;
    }

    .greeting {
        text-align: center;
        margin-top: 40px;
        font-size: 36px;
        color: #666;
    }

    .index_btn_root {
        justify-content: center;
        align-items: center;
        flex-direction: row;
        flex-wrap: wrap;
    }

    .index_btn_group {
        padding: 20px;
        justify-content: center;
        align-items: center;
        background-color: #F9F9F9;
        border-radius: 12px;
        border-color: #ccc;
        border-width: 1px;
        border-style: solid;
        width: 280px;
        height: 280px;
    }

    .index_btn_label {
        color: #666;
        font-size: 32px;
        text-align: center;
        margin-top: 30px;
    }
</style>
