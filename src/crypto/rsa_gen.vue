<template>
    <scroller class="wrapper" show-scrollbar="false">
        <div style="height: 40px;"></div>
        <div class="title_root">
            <div class="tdot"></div>
            <text class="tlab">RSA 2048 Private</text>
        </div>
        <div class="pannel">
            <text class="content">{{pemPriv}}</text>
        </div>
        <div class="title_root">
            <div class="tdot"></div>
            <text class="tlab">RSA 2048 Public</text>
        </div>
        <div class="pannel">
            <text class="content">{{pemPub}}</text>
        </div>
        <div class="title_root">
            <div class="tdot"></div>
            <text class="tlab">modulus</text>
        </div>
        <div class="pannel">
            <text class="content">{{n}}</text>
        </div>
        <div class="title_root">
            <div class="tdot"></div>
            <text class="tlab">public exponent</text>
        </div>
        <div class="pannel">
            <text class="content">{{e}}</text>
        </div>
        <div class="title_root">
            <div class="tdot"></div>
            <text class="tlab">private exponent</text>
        </div>
        <div class="pannel">
            <text class="content">{{d}}</text>
        </div>
        <div class="title_root">
            <div class="tdot"></div>
            <text class="tlab">Prime P</text>
        </div>
        <div class="pannel">
            <text class="content">{{p}}}</text>
        </div>
        <div class="title_root">
            <div class="tdot"></div>
            <text class="tlab">Prime Q</text>
        </div>
        <div class="pannel">
            <text class="content">{{q}}</text>
        </div>
        <div class="title_root">
            <div class="tdot"></div>
            <text class="tlab">Prime Exponent P</text>
        </div>
        <div class="pannel">
            <text class="content">{{dp}}</text>
        </div>
        <div class="title_root">
            <div class="tdot"></div>
            <text class="tlab">Prime Exponent Q</text>
        </div>
        <div class="pannel">
            <text class="content">{{dq}}</text>
        </div>
        <div class="title_root">
            <div class="tdot"></div>
            <text class="tlab">Crt Coefficient</text>
        </div>
        <div class="pannel">
            <text class="content">{{qinv}}</text>
        </div>
        <div style="height: 40px;"></div>
    </scroller>
</template>

<script>
    const crypto = weex.requireModule("crypto");
    module.exports = {
        data: {
            pemPriv: 'SDK版本太低，不支持',
            pemPub: 'SDK版本太低，不支持',
            n: 'SDK版本太低，不支持',
            e: 'SDK版本太低，不支持',
            d: 'SDK版本太低，不支持',
            p: 'SDK版本太低，不支持',
            q: 'SDK版本太低，不支持',
            dp: 'SDK版本太低，不支持',
            dq: 'SDK版本太低，不支持',
            qinv: 'SDK版本太低，不支持'
        },
        created() {
            if(parseInt(WXEnvironment.weexVersionCode) < 2802) {
                // SDK版本太低
                return;
            }
            this.runAlg();
        },
        methods: {
            runAlg() {
                crypto.genRSAKeypair({
                    strength: 2048,
                    publicExponent: 3,
                    pemType: 'PKCS#1',
                }, (e) => {
                    this.pemPriv = e.pemPrivate;
                    this.pemPub = e.pemPublic;
                    this.n = e.n;
                    this.e = e.e;
                    this.d = e.d;
                    this.p = e.p;
                    this.q = e.q;
                    this.dp = e.dp;
                    this.dq = e.dq;
                    this.qinv = e.qinv;
                });
            }
        }
    }
</script>

<style scoped>
    .wrapper {
        background-color: white;
    }
    .title_root {
        flex-direction: row;
        align-items: center;
        padding-left: 40px;
        padding-right: 40px;
    }
    .tdot {
        width: 20px;
        height: 20px;
        background-color: #0088fb;
        border-radius: 10px;
    }
    .tlab {
        font-size: 32px;
        font-weight: bold;
        margin-left: 20px;
    }
    .pannel {
        flex-direction: column;
        margin-top: 20px;
        margin-bottom: 20px;
        background-color: #F2F2F2;
        border-radius: 10px;
        padding: 40px;
        margin-left: 40px;
        margin-right: 40px;
    }
    .content {
        font-size: 26px;
        color: #666;
    }
</style>