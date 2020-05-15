<template>
    <div class="wrapper">
        <mpwx-btn class="btn" label="显示遮罩" id="0" @onBtnClicked="showMask"></mpwx-btn>
        <mpwx-btn class="btn" label="显示遮罩带动画" id="1" @onBtnClicked="showMaskWithAnim"></mpwx-btn>

        <mask ref="maskref" :hack="buildShow"
              @click="hideMask" @visiblechanged="visiblechanged" class="mask" v-if="show">
            <div class="cc">
                <image :src="logo" class="logo"/>
                <text class="greeting">欢迎使用MPWeex</text>
            </div>
        </mask>
    </div>
</template>

<script>
    import MpwxBtn from "../mpwx-btn"
    module.exports = {
        components : {MpwxBtn},
        data: {
            defText: "senior components and modules",
            show: false,
            hasAnimation: false,
            timingFunction: ['ease-in', 'ease-out'],
            logo: 'https://gw.alicdn.com/tfs/TB1yopEdgoQMeJjy1XaXXcSsFXa-640-302.png'
        },
        computed: {
            buildShow() {
                const { show, hasAnimation } = this;
                hasAnimation && setTimeout(() => {
                    this.appearMask(show);
                }, 50);
                return show;
            }
        },
        methods: {
            showMask(event) {
                this.show = true;
                this.hasAnimation = false;
                // this.appearMask(true);
            },
            showMaskWithAnim(event) {
                this.show = true;
                this.hasAnimation = true;
                setTimeout(() => {
                    this.appearMask(true);
                }, 50);
            },
            hideMask(event) {
                // this.show = false;
                this.appearMask(false);
            },
            visiblechanged(event) {
                const {visible} = event;
                this.show = visible;
            },
            appearMask (isOpen) {
                const { hasAnimation, timingFunction } = this;
                var self = this;
                const maskEl = self.$refs.maskref;
                if (hasAnimation && maskEl) {
                    // this.show = true;
                    animation.transition(maskEl, {
                        styles: {
                            opacity: isOpen ? 1 : 0
                        },
                        duration: 300,
                        timingFunction: timingFunction[isOpen ? 0 : 1],
                        delay: 0
                    }, function () {
                        self.show = isOpen;
                    });
                } else {
                    // this.show = isOpen;
                }
            }
        }
    }
</script>

<style scoped>
    .wrapper {
        padding: 40px;
    }

    .mask {
        justify-content: center;
        align-items: center;
        backgroundColor: rgba(0,0,0,0.5);
    }

    .cc {
        background-color: white;
        border-radius: 40px;
        padding: 40px;
    }

    .logo {
        width: 424px;
        height: 200px;
    }

    .btn {
        margin-bottom: 12px;
        margin-top: 12px;
    }

    .greeting {
        text-align: center;
        margin-top: 10px;
        font-size: 48px;
        color: #41B883;
    }
</style>