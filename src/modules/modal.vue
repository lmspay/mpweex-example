<template>
    <div class="wrapper">
        <mpwx-btn class="btn" label="toast" id="0" @onBtnClicked="onClicked"></mpwx-btn>
        <mpwx-btn class="btn" label="alert" id="1" @onBtnClicked="onClicked"></mpwx-btn>
        <mpwx-btn class="btn" label="confirm" id="2" @onBtnClicked="onClicked"></mpwx-btn>
        <mpwx-btn class="btn" label="prompt" id="3" @onBtnClicked="onClicked"></mpwx-btn>
        <mpwx-btn class="btn" label="progress" id="4" @onBtnClicked="onClicked"></mpwx-btn>
    </div>
</template>

<script>
    import MpwxBtn from "../mpwx-btn"
    var modal = weex.requireModule('modal');
    export default {
        components: {MpwxBtn},
        methods: {
            onClicked(event) {
                const {id} = event;
                switch (id) {
                    case "0":
                        modal.toast({
                            message: "toast test",
                            gravity: "center",
                            duration: 1
                        });
                        break;
                    case "1":
                        modal.alert({
                            // title: "title",
                            message: 'This is a alert',
                            okTitle: 'ok label'
                        }, function (value) {
                            modal.toast({
                                message: `${value} clicked`
                            });
                        });
                        break;
                    case "2":
                        modal.confirm({
                            title: "title",
                            message: 'Do you confirm?',
                            okTitle: 'ok label',
                            cancelTitle: 'cancel label'
                        }, function (value) {
                            modal.toast({
                                message: `${value} clicked`
                            });
                        });
                        break;
                    case "3":
                        modal.prompt({
                            title: "title",
                            message: 'This is a prompt',
                            // default: 'default text',
                            hint: 'hint text',
                            okTitle: 'ok label',
                            cancelTitle: 'cancel label'
                        }, function (res) {
                            modal.toast({
                                message: `${res.result} : ${res.data}`
                            });
                        });
                        break;
                    case "4":
                        modal.progress({
                            // cancelable: false,
                            message: '正在加载...'
                        }, function (value) {
                            modal.toast({
                                message: `${value}`
                            });
                        });

                        setTimeout(function () {
                            modal.dismiss();
                        }, 2000);
                        break;
                }
            }
        }
    }
</script>

<style scoped>
    .wrapper {
        flex: 1;
        padding: 40px;
    }
    .btn {
        margin-bottom: 12px;
        margin-top: 12px;
    }
</style>