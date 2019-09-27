<template>
    <div class="wrapper">
        <scroller class="sc">
            <text class="split">普通API</text>
            <mpwx-btn v-for="item in defList" :key="item.index"
                       :label="item.label" :id="item.index" @onBtnClicked="onButtonClicked"
                      style="width: 670px;margin-bottom: 12px; margin-top: 12px;">
            </mpwx-btn>
            <text class="split">高级API</text>
            <mpwx-btn v-for="item in defSeniorList" :key="item.index"
                      :label="item.label" :id="item.index" @onBtnClicked="onButtonClicked"
                      style="width: 670px;margin-bottom: 12px; margin-top: 12px;">
            </mpwx-btn>
            <div style="margin-bottom: 12px;"></div>
        </scroller>
    </div>
</template>

<script>
    import MpwxBtn from "../mpwx-btn"
    import MpwxSplit from "../mpwx-split"
    var navigator = weex.requireModule('navigator');
    var modal = weex.requireModule('modal');
    export default {
        components : {MpwxBtn, MpwxSplit},
        data: {
            defList: [
                {index: 0, label: "返回上一级"},
                {index: 1, label: "设置标题"},
                {index: 2, label: "跳转新页面"},
                {index: 3, label: "显示加载动画"},
                {index: 4, label: "隐藏加载动画"},
            ],
            defSeniorList: [
                {index: 5, label: "显示标题栏"},
                {index: 6, label: "隐藏标题栏"},
                {index: 7, label: "设置标题样式"},
            ]
        },
        methods: {
            onButtonClicked (e) {
                const { id, label } = e;
                switch (id) {
                    case 0: // 返回上一级
                        navigator.pop();
                        break;
                    case 1: // 设置标题
                        navigator.setNavBarTitle('demo title' + parseInt(Math.random() * 100));
                        break;
                    case 2: // 跳转新页面
                        navigator.push({
                            page: '/modules/navnewpage.js',
                            // hideNavBar: true,
                            title: "新页面"
                        });
                        break;
                    case 3: // 显示加载动画
                        navigator.showNavBarIndicator();
                        break;
                    case 4: // 隐藏加载动画
                        navigator.hideNavBarIndicator();
                        break;
                    case 5: // 显示标题栏
                        navigator.setNavBarHidden({hidden: 0}, function (msg) {
                        });
                        break;
                    case 6: // 隐藏标题栏
                        navigator.setNavBarHidden({hidden: 1}, function (msg) {
                        });
                        break;
                    case 7: // 设置标题样式
                        navigator.setupTitleBarTheme({
                            navBarTintColor: '#FF0000', // 标题字体颜色
                            navBarRightBgColor: '#FFFFFF', // 右侧按钮容器背景颜色
                            navBarRigntBorderWidth: 4, // 右侧按钮容器边框大小
                            navBarRigntBorderColor: '#000000', // 右侧按钮容器边框颜色
                            navBarRightSplitColor: '#FF0000', // 右侧按钮容器分隔线颜色
                            navBarBgColor: '#1Ab700', // 标题栏颜色
                            statusBarBgColor: '#17A05A', // 状态栏颜色
                        });
                        break;
                }
            }
        }
    }
</script>

<style scoped>
    .wrapper {
        justify-content: center;
        align-items: center;
    }
    .sc {
        width: 750px;
        align-items: center;
    }
    .split {
        background-color: #eee;
        font-size: 26px;
        height: 60px;
        padding-left: 40px;
        line-height: 60px;
        color: #666;
        width: 750px;
    }
</style>