<template>
    <scroller  show-scrollbar="false">
        <div class="group">
            <mpwx-btn class="btn" label='生成二维码' id="1" @onBtnClicked="gen"></mpwx-btn>
            <mpwx-btn class="btn" label='生成二维码（Base64数据）' id="2" @onBtnClicked="gen2"></mpwx-btn>
        </div>

        <image ref="img" class="image" autoBitmapRecycle="false"></image>
    </scroller>
</template>

<script>
    const qrcode = weex.requireModule('qrcode');
    var modal = weex.requireModule('modal');

    import MpwxBtn from "../mpwx-btn"
    export default {
        components : {MpwxBtn},
        data() {
            return {
                value: '---'
            }
        },
        methods: {
            gen() {
                var self = this;
                self.value = '---';
                qrcode.gen(self.$refs.img, {
                    content: "Hello, World!",
                    size: 200,
                    color: '#41B883',
                    logo: 'http://cs.txmpay.com:28080/logo_a.png'
                }, (e) => {
                   if(e.result === 'cancel') {
                       modal.toast({
                           message: "gen qrcode failed.",
                           gravity: "bottom",
                           duration: 1
                       });
                   }
                });
            },
            gen2() {
                var self = this;
                self.value = '---';
                qrcode.gen(self.$refs.img, {
                    content: "bG1zcGF5LmNvbQ==",
                    size: 200,
                    type: "base64"
                }, (e) => {
                    if(e.result === 'cancel') {
                        modal.toast({
                            message: "gen qrcode failed.",
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
    .group {
        flex-direction: column;
        width: 650px;
        margin-left: 50px;
        margin-top: 50px;
    }
    .image {
        min-width: 400px;
        min-height: 400px;
        margin-top: 50px;
        align-self: center;
        width: 200px;
        height: 200px;
    }
    .btn {
        margin-bottom: 12px;
        margin-top: 12px;
    }
</style>