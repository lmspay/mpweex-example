<template>
    <div class="container">
        <text style="margin-bottom: 20px; font-size: 32px;">action value: {{value}}, index : {{index}}</text>
        <mpwx-btn label="Create Action" id="0" @onBtnClicked="createAction"></mpwx-btn>
    </div>
</template>

<style>
    .container{
        flex: 1;
        padding: 40px;
    }
</style>

<script>
    import MpwxBtn from "../mpwx-btn"
    const actionSheet = weex.requireModule('actionSheet');
    module.exports = {
        components : {MpwxBtn},
        data: {
            value: '',
            index: -1
        },
        methods: {
            createAction: function() {
                var items = [
                    {'type': 0,'message':'确认'},
                    {'type': 1,'message':'取消'},
                    {'type': 2,'message':'删除'}
                ];

                var self = this;
                actionSheet.create({
                    'items':items,
                    'title':'提示',
                    'message':'欢迎使用两码事小程序'
                }, function (ret) {
                    var result = ret.result;
                    if(result == 'success') {
                        self.value = ret.data.message;
                        self.index = ret.data.index;
                    }else if(result == 'cancel') {
                        self.value = '取消';
                        self.index = -1;
                    }else if(result == 'error') {
                        self.value = ret.data;
                        self.index = -1;
                    }
                });
            }
        }
    }
</script>