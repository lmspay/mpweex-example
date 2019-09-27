<template>
    <div class="wrapper">
        <div class="title_root">
            <div class="tdot"></div>
            <text class="tlab">Simple Sms</text>
        </div>
        <div class="pannel" @click="onSimpleSms">
            <text class="cme">click me</text>
            <text class="content">sms.invoke(['10010']);</text>
        </div>

        <div class="title_root">
            <div class="tdot"></div>
            <text class="tlab">Multiple recipients</text>
        </div>
        <div class="pannel" @click="onMultipleSms">
            <text class="cme">click me</text>
            <text class="content">sms.invoke(['10010', '10086']);</text>
        </div>

        <div class="title_root">
            <div class="tdot"></div>
            <text class="tlab">Sms with content and callback</text>
        </div>
        <div class="pannel" @click="onContentSms">
            <text class="cme">click me</text>
<text class="content">sms.invoke(['10010'],
    'message goes here.', (e) => {
    if(e.result == 'success') {
        modal.toast({
            message: "sms sent",
            gravity: "bottom",
            duration: 1
        });
    }
});</text>
        </div>
    </div>
</template>

<script>
    var modal = weex.requireModule('modal');
    var sms = weex.requireModule('sms');
    module.exports = {
        data: {
        },
        methods: {
            onSimpleSms() {
                sms.invoke(['10010']);
            },
            onMultipleSms() {
                sms.invoke(['10010', '10086']);
            },
            onContentSms() {
                sms.invoke(['10010'],
                    'message goes here.', (e) => {
                    if(e.result == 'success') {
                        modal.toast({
                            message: "sms sent",
                            gravity: "bottom",
                            duration: 1
                        });
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
    .cme {
        font-size: 24px;
        color: #CCC;
        align-self: flex-end;
        position: absolute;
        right: 20px;
        top: 20px;
    }
    .content {
        font-size: 26px;
        color: #666;
    }
</style>