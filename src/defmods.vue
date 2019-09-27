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
    module.exports = {
        components : {MpwxCell},
        data() {
            var arrr = [
                {label: "基础", isSplit: true},
                {label: "导航 (Navigator)", icon: "", windowTitle: "Navigator", href: "/modules/navigator.js"},
                {label: "上拉菜单 (ActionSheet)", icon: "", windowTitle: "ActionSheet", href: "/modules/actionsheet.js"},
                {label: "模态框 (Modal)", icon: "", windowTitle: "Modal", href: "/modules/modal.js"},
                {label: "自定义字体 (Custom Font)", icon: "", windowTitle: "Custom Font", href: "/modules/customfont.js"},
                {label: "文档对象模型 (Dom)", icon: "", windowTitle: "Dom", href: "/modules/dom.js"},
                {label: "动画 (Animation)", icon: "", windowTitle: "Animation", href: "/modules/animation.js"},
                {label: "选择器 (Picker)", icon: "", windowTitle: "Picker", href: "/modules/picker.js"},

                {label: "设备", isSplit: true},
                {label: "屏幕 (Screen)", icon: "", windowTitle: "Screen", href: "/modules/screen.js"},
                {label: "振动 (Vibration)", icon: "", windowTitle: "Vibration", href: "/modules/vibration.js"},
                {label: "音量 (Volume)", icon: "", windowTitle: "Volume", href: "/modules/volume.js"},
                {label: "电量 (Battery)", icon: "", windowTitle: "Battery", href: "/modules/battery.js"},

                {label: "网络", isSplit: true},
                {label: "浏览器 (Webview)", icon: "", windowTitle: "Webview", href: "/modules/webview.js"},
                {label: "网络套接字 (WebSocket)", icon: "", windowTitle: "WebSocket", href: "/modules/websocket.js"},
                {label: "网络请求 (Stream)", icon: "", windowTitle: "Stream", href: "/modules/stream.js"},
                {label: "网络信息 (Network)", icon: "", windowTitle: "Network", href: "/modules/network.js"},

                {label: "系统", isSplit: true},
                {label: "粘贴板 (Clipboard)", icon: "", windowTitle: "Clipboard", href: "/modules/clipboard.js"},
                {label: "存储 (Storage)", icon: "", windowTitle: "Storage", href: "/modules/storage.js"},
                {label: "语言及地区 (Locale)", icon: "", windowTitle: "Locale", href: "/modules/locale.js"},
            ];
            if("android" == WXEnvironment.platform) {
                arrr.push({label: "权限 (Permissions)", icon: "", windowTitle: "Permissions", href: "/modules/permissions.js"});
            }
            return {
                defList: arrr
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
    }
</style>