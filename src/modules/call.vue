<template>
    <div class="wrapper">
        <div class="title_root">
            <div class="tdot"></div>
            <text class="tlab">Simple Call</text>
        </div>
        <div class="pannel" @click="onSimpleCall">
            <text class="cme">click me</text>
            <text class="content">call.invoke('10010');</text>
        </div>

        <div class="title_root">
            <div class="tdot"></div>
            <text class="tlab">Call with callback</text>
        </div>
        <div class="pannel" @click="onCallbackCall">
            <text class="cme">click me</text>
<text class="content">call.invoke('10010', (e) => {
    if(e.result == 'success') {
        modal.toast({
            message: "called",
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
    var call = weex.requireModule('call');
    module.exports = {
        data: {
        },
        methods: {
            onSimpleCall() {
                call.invoke('10010');
            },
            onCallbackCall() {
                call.invoke('10010', (e) => {
                    if(e.result == 'success') {
                        modal.toast({
                            message: "called",
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