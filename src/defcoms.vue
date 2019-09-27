<template>
    <div class="wrapper">
        <scroller class="sc" show-scrollbar="false">
            <mpwx-cell v-for="item in defList" :key="item.label"
                       :label="item.label"
                       :icon="item.icon"
                       :windowTitle="item.windowTitle"
                       :href="item.href"
                       :isSplit="item.isSplit">
            </mpwx-cell>
        </scroller>
    </div>
</template>

<script>
    import MpwxCell from "./mpwx-cell"
    var navigator = weex.requireModule('navigator');
    module.exports = {
        components : {MpwxCell},
        data: {
            defList: [
                {label: "内置组件", isSplit: true},
                {label: "容器 (div)", icon: "", windowTitle: "div", href: "/components/div.js"},
                {label: "文本 (text)", icon: "", windowTitle: "text", href: "/components/text.js"},
                // {label: "富文本 (richtext)", icon: "", windowTitle: "richtext", href: "/components/richtext.js"},
                {label: "文本框 (textarea)", icon: "", windowTitle: "textarea", href: "/components/textarea.js"},
                {label: "开关 (switch)", icon: "", windowTitle: "switch", href: "/components/switch.js"},
                {label: "图像 (image)", icon: "", windowTitle: "image", href: "/components/image.js"},
                {label: "输入框 (input)", icon: "", windowTitle: "input", href: "/components/input.js"},
                {label: "滚动 (scroller)", icon: "", windowTitle: "scroller", href: "/components/scroller.js"},
                {label: "列表 (list)", icon: "", windowTitle: "list", href: "/components/list.js"},
                {label: "复用列表 (recycle-list)", icon: "", windowTitle: "recycle-list", href: "/components/recycle-list.js"},
                {label: "轮播 (slider)", icon: "", windowTitle: "slider", href: "/components/slider.js"},
                {label: "无限轮播 (sliderinfinite)", icon: "", windowTitle: "sliderinfinite", href: "/components/sliderinfinite.js"},
                {label: "视频 (video)", icon: "", windowTitle: "video", href: "/components/video.js"},
                {label: "瀑布流 (waterfall)", icon: "", windowTitle: "waterfall", href: "/components/waterfall.js"},
                // {label: "遮罩 (mask)", icon: "", windowTitle: "mask", href: "/components/mask.js"},
                {label: "浏览器 (web)", icon: "", windowTitle: "web", href: "/components/web.js"},
                // {label: "扩展组件", isSplit: true},
                // {label: "marquee", icon: "", windowTitle: "marquee", href: "/components/marquee.js"},
                // {label: "tabbar", icon: "", windowTitle: "tabbar", href: "/components/tabbar.js"},
                // {label: "countdown", icon: "", windowTitle: "countdown", href: "/components/countdown.js"},
            ]
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
    }
</style>