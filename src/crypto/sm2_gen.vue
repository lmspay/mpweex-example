<template>
    <scroller class="wrapper" show-scrollbar="false">
        <div style="height: 40px;"></div>
        <div class="title_root">
            <div class="tdot"></div>
            <text class="tlab">SM2 Private</text>
        </div>
        <div class="pannel">
            <text class="content">{{priv}}</text>
        </div>
        <div class="title_root">
            <div class="tdot"></div>
            <text class="tlab">SM2 Public</text>
        </div>
        <div class="pannel">
            <text class="content">{{pub}}</text>
        </div>
        <div class="title_root">
            <div class="tdot"></div>
            <text class="tlab">SM2 Compressed Public</text>
        </div>
        <div class="pannel">
            <text class="content">{{comPub}}</text>
        </div>
    </scroller>
</template>

<script>
    const crypto = weex.requireModule("crypto");
    module.exports = {
        data: {
            priv: 'SDK版本太低，不支持',
            pub: 'SDK版本太低，不支持',
            comPub: 'SDK版本太低，不支持'
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
                crypto.genSM2Keypair({
                }, (e) => {
                    this.priv = e.privateKey;
                    this.pub = e.publicKey;
                    this.comPub = e.compressedPublicKey;
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