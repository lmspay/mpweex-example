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
                {label: "Base64算法", icon: "", windowTitle: "Base64", href: "/crypto/base64.js"},
                {label: "摘要算法", icon: "", windowTitle: "Digest", href: "/crypto/digest.js"},
                {label: "对称加解密算法", icon: "", windowTitle: "Symmetric", href: "/crypto/symmetric.js"},
                {label: "Hmac算法", icon: "", windowTitle: "Hmac", href: "/crypto/hmac.js"},
                {label: "DES其它算法", icon: "", windowTitle: "DES Extend", href: "/crypto/des.js"},
                {label: "非对称", isSplit: true},
                {label: "RSA密钥生成", icon: "", windowTitle: "RSA Generator", href: "/crypto/rsa_gen.js"},
                {label: "SM2密钥生成", icon: "", windowTitle: "SM2 Generator", href: "/crypto/sm2_gen.js"},
                {label: "RSA加解密", icon: "", windowTitle: "RSA", href: "/crypto/rsa.js"},
                {label: "SM2加解密", icon: "", windowTitle: "SM2", href: "/crypto/sm2.js"},
                {label: "RSA签名验签", icon: "", windowTitle: "RSA Sign", href: "/crypto/rsa_sign.js"},
                {label: "SM2签名验签", icon: "", windowTitle: "SM2 Sgn", href: "/crypto/sm2_sign.js"},
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