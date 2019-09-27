
<template>
    <scroller>
        <div>
            <text class="split">websocket</text>

            <input type="text" placeholder="please input message to send" class="input" autofocus="false" value="" @change="onchange" @input="oninput" ref="input"/>

            <div style="flex-direction: row; justify-content: center; margin-top: 20px;">
                <text class="button" @click="connect">connect</text>
                <text class="button" @click="send">send</text>
                <text class="button" @click="close">close</text>
            </div>

            <text class="split" style="margin-top: 20px;">method = send</text>
            <text class="tip">{{sendinfo}}</text>

            <text class="split" style="margin-top: 20px;">method = onopen</text>
            <text class="tip">{{onopeninfo}}</text>

            <text class="split" style="margin-top: 20px;">method = onmessage</text>
            <text class="tip">{{onmessage}}</text>

            <text class="split" style="margin-top: 20px;">method = onclose</text>
            <text class="tip">{{oncloseinfo}}</text>

            <text class="split" style="margin-top: 20px;">method = onerror</text>
            <text class="tip">{{onerrorinfo}}</text>
        </div>

    </scroller>
</template>

<style scoped>
    .input {
        font-size: 40px;
        height: 80px;
        margin: 26px;
        border-color: gray;
        border-width: 1px;
        padding: 8px;
    }
    .tip {
        color: black;
        height: 80px;
        font-size: 32px;
        padding-left: 26px;
        line-height: 80px;
    }
    .button {
        font-size: 36px;
        width: 150px;
        color: #41B883;
        text-align: center;
        padding-top: 25px;
        padding-bottom: 25px;
        border-width: 2px;
        border-style: solid;
        margin-right: 20px;
        border-color: rgb(162, 217, 192);
        background-color: rgba(162, 217, 192, 0.2);
    }
    .split {
        background-color: #eee;
        font-size: 26px;
        height: 60px;
        padding-left: 26px;
        line-height: 60px;
        color: #666;
    }
</style>


<script>
    var websocket = weex.requireModule('webSocket')
    export default {
        data () {
            return {
                connectinfo: '',
                sendinfo: '',
                onopeninfo: '',
                onmessage: '',
                oncloseinfo: '',
                onerrorinfo: '',
                closeinfo: '',
                txtInput:'',
                navBarHeight: 88,
                title: 'Navigator',
                dir: 'examples',
                baseURL: ''
            }
        },
        created() {
            var self = this;
            websocket.onopen(function (e) {
                self.onopeninfo = 'websocket open';
            });
            websocket.onmessage(function (e) {
                self.onmessage = e.data;
            });
            websocket.onerror(function (e) {
                self.onerrorinfo = e.data;
            });
            websocket.onclose(function (e) {
                self.onopeninfo = '';
                self.oncloseinfo = e.code;
            });
        },
        methods: {
            connect:function() {
                websocket.WebSocket('ws://echo.websocket.org','');
                this.onopeninfo = 'connecting...';
            },
            send:function(e) {
                var input = this.$refs.input;
                input.blur();
                websocket.send(this.txtInput);
                this.sendinfo = this.txtInput;
            },
            oninput: function(event) {
                this.txtInput = event.value;
            },
            close:function(e) {
                websocket.close();
            },
        },
    }
</script>
