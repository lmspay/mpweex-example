<template>
    <div>
    <div class="container">
        <text style="margin-bottom: 20px; font-size: 32px;">clipboard value: {{value}}</text>
        <mpwx-btn class="btn" label='复制 "test copy"' id="0" @onBtnClicked="createAction"></mpwx-btn>
        <mpwx-btn class="btn" label='获取' id="1" @onBtnClicked="createAction"></mpwx-btn>
    </div>
        <text class="split">测试粘贴</text>
        <div class="container">
            <input class="edit" placeholder="请粘贴..." />
        </div>
    </div>
</template>

<style>
    .container{
        padding: 40px;
    }
    .btn {
        margin-bottom: 12px;
        margin-top: 12px;
    }
    .split {
        background-color: #eee;
        font-size: 26px;
        height: 60px;
        padding-left: 40px;
        line-height: 60px;
        color: #666;
    }
    .edit {
        height: 80px;
        border-color: #a2a2a2;
        border-width: 1px;
        padding: 8px;
    }
</style>

<script>
    import MpwxBtn from "../mpwx-btn"
    const clipboard = weex.requireModule('clipboard')
    export default {
        components : {MpwxBtn},
        data: {
            value: ''
        },
        methods: {
            createAction: function(e) {
                const {id} = e;
                var self = this;
                switch (id) {
                    case "0":
                        var v = parseInt(Math.random() * 100);
                        clipboard.setString("test copy");
                        break;
                    case "1":
                        clipboard.getString(function (res) {
                            self.value = `${res.result} , ${res.data}`;
                        });
                        break;
                }
            }
        }
    }
</script>