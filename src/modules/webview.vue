<template>
    <div class="wrapper">
        <web ref="webview" style="width: 730px; height: 500px" src="https://vuejs.org"
             @pagestart="onPageStart" @pagefinish="onPageFinish" @error="onError" @receivedtitle="onReceivedTitle"></web>
        <div class="row" style="padding-top: 10px">
            <text class="button" :class="[canGoBack ? 'button-enabled' : 'button-disabled']" @click="goBack">←</text>
            <text class="button" :class="[canGoForward ? 'button-enabled' : 'button-disabled']" @click="goForward">→</text>
            <text class="button" @click="reload">reload</text>
        </div>
        <text style="font-size: 32px; margin-top: 16px;" test-id='pagestart'>pagestart: {{pagestart}}</text>
        <text style="font-size: 32px; margin-top: 16px;" test-id='pagefinish'>pagefinish: {{pagefinish}}</text>
        <text style="font-size: 32px; margin-top: 16px;" test-id='title'>title: {{title}}</text>
        <text style="font-size: 32px; margin-top: 16px;" test-id='error'>error: {{error}}</text>
    </div>
</template>

<style scoped>
    .wrapper {
        flex-direction: column;
        padding: 10px;
    }
    .row {
        flex-direction: row;
        justify-content: space-between
    }
    .button {
        color: #fff;
        background-color: #337ab7;
        border-color: #2e6da4;
        border-radius: 12px;
        padding-top: 20px;
        padding-left: 36px;
        padding-bottom: 20px;
        padding-right: 36px;
        font-size: 36px;
        text-align: center;
        font-weight: 500;
        margin-bottom: 10px;
    }
    .button-enabled {
        opacity: 1;
    }
    .button-disabled {
        opacity: 0.65;
    }
</style>

<script>
    var webview = weex.requireModule('webview');
    module.exports = {
        data: {
            pagestart: '',
            pagefinish: '',
            title: '',
            error: '',
            canGoBack: false,
            canGoForward: false,
        },
        methods: {
            goBack: function() {
                webview.goBack(this.$refs.webview);
            },
            goForward: function() {
                webview.goForward(this.$refs.webview);
            },
            reload: function() {
                webview.reload(this.$refs.webview);
            },
            onPageStart: function(e) {
                this.pagestart = e.url;
            },
            onPageFinish: function(e) {
                this.pagefinish = e.url;
                this.canGoBack = e.canGoBack;
                this.canGoForward = e.canGoForward;
                if (e.title) {
                    this.title = e.title;
                }
            },
            onError: function(e) {
                this.error = url;
            },
            onReceivedTitle: function(e) {
                this.title = e.title;
            }
        }
    }
</script>