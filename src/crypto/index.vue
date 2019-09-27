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
    import MpwxCell from "../mpwx-cell"
    module.exports = {
        components : {MpwxCell},
        data: {
            defList: [
                {label: "通用算法", icon: "", windowTitle: "Common", href: "/crypto/common.js"},
                {label: "Hash", icon: "", windowTitle: "Hash", href: "/crypto/hash.js"},
                {label: "国密SMS4", icon: "", windowTitle: "SMS4", href: "/crypto/sms4.js"},
                {label: "AES", icon: "", windowTitle: "AES", href: "/crypto/aes.js"},
                {label: "DES", icon: "", windowTitle: "DES", href: "/crypto/des.js"},
                {label: "MAC", icon: "", windowTitle: "MAC", href: "/crypto/mac.js"},
                {label: "非对称", isSplit: true},
                {label: "RSA", icon: "", windowTitle: "RSA", href: "/crypto/rsa.js"},
                {label: "国密SM2", icon: "", windowTitle: "SM2", href: "/crypto/sm2.js"},
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