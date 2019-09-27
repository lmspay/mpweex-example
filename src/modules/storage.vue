<template>
    <div>
        <div class="group center">
            <div class="panel"><text class="text">{{state}}</text></div>
        </div>
        <div class="group">
            <mpwx-btn class="btn" label='设置 (key=name)' id="0" @onBtnClicked="setItem"></mpwx-btn>
            <mpwx-btn class="btn" label='获取' id="1" @onBtnClicked="getItem"></mpwx-btn>
            <mpwx-btn class="btn" label='删除' id="2" @onBtnClicked="removeItem"></mpwx-btn>
            <mpwx-btn class="btn" label='获取所有key' id="3" @onBtnClicked="getAll"></mpwx-btn>
        </div>
    </div>
</template>

<script>
    const storage = weex.requireModule('storage')
    const modal = weex.requireModule('modal')
    import MpwxBtn from "../mpwx-btn"
    export default {
        components : {MpwxBtn},
        data () {
            return {
                keys: '[]',
                length: 0,
                state: '----'
            }
        },
        methods: {
            setItem () {
                storage.setItem('name', 'Hanks', event => {
                    this.state = 'set success'
                    console.log('set success')
                })
            },
            getItem () {
                storage.getItem('name', event => {
                    console.log('get value:', event.data)
                    this.state = 'value: ' + event.data
                })
            },
            removeItem () {
                storage.removeItem('name', event => {
                    console.log('delete value:', event.data)
                    this.state = 'deleted'
                })
            },
            getAll () {
                storage.getAllKeys(event => {
                    // modal.toast({ message: event.result })
                    if (event.result === 'success') {
                        modal.toast({
                            message: 'props: ' + event.data.join(', ')
                        })
                    }
                })
            }
        }
    }
</script>

<style scoped>
    .panel {
        height: 100px;
        flex-direction: column;
        justify-content: center;
        border-width: 2px;
        border-style: solid;
        border-color: rgb(162, 217, 192);
        background-color: rgba(162, 217, 192, 0.2);
    }
    .group {
        flex-direction: column;
        width: 650px;
        margin-left: 50px;
        margin-top: 50px;
    }
    .center {
        justify-content: center;
    }
    .text {
        font-size: 50px;
        text-align: center;
        padding-left: 25px;
        padding-right: 25px;
        color: #41B883;
    }
    .btn {
        margin-bottom: 12px;
        margin-top: 12px;
    }
</style>