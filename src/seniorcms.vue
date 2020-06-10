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
        data: {
            defList: [
                // {label: "Audio-", icon: "", windowTitle: "Audio", href: "/modules/audio.js"},
                // {label: "AudioRecorder-", icon: "", windowTitle: "AudioRecorder", href: "/modules/audiorecorder.js"},
                {label: "扫一扫 (Scan)", icon: "", windowTitle: "Scan", href: "/modules/scan.js"},
                {label: "二维码 (Qrcode)", icon: "", windowTitle: "Qrcode", href: "/modules/qrcode.js"},
                {label: "拨号 (Call)", icon: "", windowTitle: "Call", href: "/modules/call.js"},
                {label: "短信 (Sms)", icon: "", windowTitle: "Sms", href: "/modules/sms.js"},
                {label: "邮件 (Email)", icon: "", windowTitle: "Email", href: "/modules/email.js"},
                {label: "定位 (Geolocation)", icon: "", windowTitle: "Geolocation", href: "/modules/geolocation.js"},
                {label: "密码算法 (Crypto)", icon: "", windowTitle: "Crypto", href: "/crypto/index.js"},
                {label: "传感器", isSplit: true},
                {label: "光线传感器 (Light)", icon: "", windowTitle: "Light", href: "/modules/light.js"},
                {label: "距离传感器 (Proximity)", icon: "", windowTitle: "Proximity", href: "/modules/proximity.js"},
                {label: "加速度传感器 (Accelerometer)", icon: "", windowTitle: "Accelerometer", href: "/modules/accelerometer.js"},
                {label: "方位角传感器 (Compass)", icon: "", windowTitle: "Compass", href: "/modules/compass.js"},
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