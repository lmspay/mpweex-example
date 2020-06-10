<template>
    <div class="wrapper">
        <div class="title_root">
            <div class="tdot"></div>
            <text class="tlab">PbocDESMac Hex</text>
        </div>
        <div class="pannel">
            <text class="content">{{pbocDESMacHexBuf}}</text>
        </div>
        <div class="title_root">
            <div class="tdot"></div>
            <text class="tlab">AnsiX9.9Mac Hex</text>
        </div>
        <div class="pannel">
            <text class="content">{{ansix9_9HexBuf}}</text>
        </div>
        <div class="title_root">
            <div class="tdot"></div>
            <text class="tlab">AnsiX9.19Mac Hex</text>
        </div>
        <div class="pannel">
            <text class="content">{{ansix9_19HexBuf}}</text>
        </div>
        <div class="title_root">
            <div class="tdot"></div>
            <text class="tlab">Diversify Hex</text>
        </div>
        <div class="pannel">
            <text class="content">{{diversifyHexBuf}}</text>
        </div>
    </div>
</template>

<script>
    const crypto = weex.requireModule("crypto");
    module.exports = {
        data: {
            pbocDESMacHexBuf: 'SDK版本太低，不支持',
            ansix9_9HexBuf: 'SDK版本太低，不支持',
            ansix9_19HexBuf: 'SDK版本太低，不支持',
            diversifyHexBuf: 'SDK版本太低，不支持'
        },
        created() {
            if(parseInt(WXEnvironment.weexVersionCode) < 2802) {
                // SDK版本太低
                return;
            }
            this.runPbocDesMac();
            this.runAnsiX9_9Mac();
            this.runAnsiX9_19Mac();
            this.runDiversifyMac();
        },
        methods: {
            runPbocDesMac() {
                crypto.desExt({
                    algorithm: 'PbocDESMac',
                    key: '6B8B4567327B23C6',
                    iv: '643C986966334873',
                    data: '616263',
                    keyType: 'hex',
                    ivType: 'hex',
                    contentType: 'hex',
                    resultType: 'hex'
                }, (e) => {
                    // 检查hex输出
                    if(e.data != '041B7BE33A472DE5') {
                        this.pbocDESMacHexBuf = '计算异常\n期望值:041B7BE33A472DE5\n实际值:' + e.data;
                    }else {
                        this.pbocDESMacHexBuf = e.data;
                    }
                });
            },
            runAnsiX9_9Mac() {
                crypto.desExt({
                    algorithm: 'AnsiX9.9Mac',
                    key: '6B8B4567327B23C6',
                    data: '616263',
                    keyType: 'hex',
                    contentType: 'hex',
                    resultType: 'hex'
                }, (e) => {
                    // 检查hex输出
                    if(e.data != 'C635A010A858E999') {
                        this.ansix9_9HexBuf = '计算异常\n期望值:C635A010A858E999\n实际值:' + e.data;
                    }else {
                        this.ansix9_9HexBuf = e.data;
                    }
                });
            },
            runAnsiX9_19Mac() {
                crypto.desExt({
                    algorithm: 'AnsiX9.19Mac',
                    key: '6B8B4567327B23C6643C986966334873',
                    data: '616263',
                    keyType: 'hex',
                    contentType: 'hex',
                    resultType: 'hex'
                }, (e) => {
                    // 检查hex输出
                    if(e.data != 'F13E7628BC539D7A') {
                        this.ansix9_19HexBuf = '计算异常\n期望值:F13E7628BC539D7A\n实际值:' + e.data;
                    }else {
                        this.ansix9_19HexBuf = e.data;
                    }
                });
            },
            runDiversifyMac() {
                crypto.desExt({
                    algorithm: 'Diversify',
                    key: '6B8B4567327B23C6643C986966334873',
                    data: '055EFB6966334873',
                    keyType: 'hex',
                    contentType: 'hex',
                    resultType: 'hex'
                }, (e) => {
                    // 检查hex输出
                    if(e.data != 'FFE8F39C6DB592D0F76E75AAEF7416B9') {
                        this.diversifyHexBuf = '计算异常\n期望值:FFE8F39C6DB592D0F76E75AAEF7416B9\n实际值:' + e.data;
                    }else {
                        this.diversifyHexBuf = e.data;
                    }
                });
            }
        }
    }
</script>

<style scoped>
    .wrapper {
        padding: 40px;
    }
    .title_root {
        flex-direction: row;
        align-items: center;
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
    }
    .content {
        font-size: 26px;
        color: #666;
    }
</style>