<template>
    <scroller class="info">
        <text class="title">Mini Program Weex SDK Version</text>
        <text class="version">{{version}}</text>
        <div class="group">
            <text class="label">SDK Version Code</text>
            <text class="value">{{versionCode}}</text>
        </div>
        <div class="group">
            <text class="label">JS Framework</text>
            <text class="value">{{jsfmVersion}}</text>
        </div>
        <div class="group">
            <text class="label">platform</text>
            <text class="value">{{platform}}</text>
        </div>
        <div class="group">
            <text class="label">osVersion</text>
            <text class="value">{{osVersion}}</text>
        </div>
        <div class="group">
            <text class="label">appGroup</text>
            <text class="value">{{appGroup}}</text>
        </div>
        <div class="group">
            <text class="label">appName</text>
            <text class="value">{{appName}}</text>
        </div>
        <div class="group">
            <text class="label">appVersion</text>
            <text class="value">{{appVersion}}</text>
        </div>
        <div class="group">
            <text class="label">deviceModel</text>
            <text class="value">{{deviceModel}}</text>
        </div>
        <div class="group">
            <text class="label">scale</text>
            <text class="value">{{scale}}</text>
        </div>
        <div class="group">
            <text class="label">resolution</text>
            <text class="value">{{resolution}}</text>
        </div>
    </scroller>
</template>

<script>
    const clipboard = weex.requireModule('clipboard');
    const modal = weex.requireModule('modal');
    const invalid = '- invalid -';
    const unknown = '- - -';

    export default {
        data () {
            return {
                version: invalid,
                versionCode: invalid,
                jsfmVersion: invalid,
                platform: invalid,
                osVersion: invalid,
                appName: invalid,
                appVersion: invalid,
                deviceModel: invalid,
                deviceWidth: invalid,
                deviceHeight: invalid,
                resolution: invalid,
                scale: invalid,
            }
        },
        created () {
            try {
                this.jsfmVersion = getJSFMVersion()
            } catch (e) {
                this.jsfmVersion = '≤ 0.15.6'
            }

            if (typeof WXEnvironment === 'object') {
                this.version = WXEnvironment.weexVersion || unknown;
                this.versionCode = WXEnvironment.weexVersionCode || unknown;
                this.platform = WXEnvironment.platform || unknown;
                this.osVersion = WXEnvironment.osVersion || unknown;
                this.appGroup = WXEnvironment.appGroup || unknown;
                this.appName = WXEnvironment.appName || unknown;
                this.appVersion = WXEnvironment.appVersion || unknown;
                this.deviceModel = WXEnvironment.deviceModel || unknown;
                this.deviceWidth = WXEnvironment.deviceWidth || unknown;
                this.deviceHeight = WXEnvironment.deviceHeight || unknown;
                this.scale = WXEnvironment.scale || unknown;
                this.resolution = this.deviceWidth + ' x ' + this.deviceHeight;
            }
        }
    }
</script>

<style scoped>
    .title {
        font-size: 40px;
        text-align: center;
        color: #888888;
        margin-top: 40px;
        margin-bottom: 20px;
    }
    .version {
        font-size: 80px;
        text-align: center;
        margin-bottom: 60px;
    }
    .group {
        margin-top: 22px;
        flex-direction: row;
    }
    .label {
        width: 300px;
        font-size: 32px;
        text-align: right;
        color: #888888;
    }
    .value {
        width: 400px;
        padding-left: 50px;
        font-size: 32px;
    }
</style>