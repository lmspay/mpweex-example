<template>
    <div class="wrapper">
        <div class="target_bg" ref="target_bg">
            <text class="target" ref="target">MPWEEX</text>
        </div>
        <text class="split">动画效果(同animate.css)</text>
        <scroller class="sc" show-scrollbar="false">
            <wxc-radio :list="anim_list"
                       @wxcRadioListChecked="wxcRadioListChecked"></wxc-radio>
            <!--<wx-picker :data="anim_data" @wxChange="handleChange"></wx-picker>-->
        </scroller>
    </div>
</template>

<script>
    const animation = weex.requireModule('animation');
    const modal = weex.requireModule('modal');
    // import WxPicker from "../wx-picker"
    import WxcRadio from "../wxc-radio"

    function animation_base(elem) {
        var colorIndex = 1;
        var colorList = ['#f35626', '#f865da', '#df89ff', '#839dff', '#5fadf9', '#4ec771', '#feab3a'];
        var action = function action() {
            animation.transition(elem, {
                styles: {
                    backgroundColor: colorList[colorIndex]
                },
                duration: 3000, //ms
                timingFunction: 'linear'
            }, function() {
                if (colorIndex < colorList.length - 1) {
                    colorIndex++;
                } else {
                    colorIndex = 0;
                }
                action();
            });
        };
        action();
    }

    // Flash
    function animation_flash(elem) {
        var opacityIndex = 0;
        var opacityList = [0, 1, 0, 1];
        var action = function action() {
            animation.transition(elem, {
                styles: {
                    opacity: opacityList[opacityIndex]
                },
                duration: 250, //ms
                timingFunction: 'ease'
            }, function() {
                if (opacityIndex < opacityList.length - 1) {
                    opacityIndex++;
                    action();
                }
            });
        };
        action();
    }

    // Shake
    function animation_shake(elem) {
        var offetIndex = 0;
        var offetList = [-20, 20, -20, 20, -20, 20, -20, 20, -20, 0];
        var action = function action() {
            animation.transition(elem, {
                styles: {
                    transform: 'translateX(' + offetList[offetIndex] + 'px)'
                },
                duration: 100, //ms
                timingFunction: 'ease-in-out'
            }, function() {
                if (offetIndex < offetList.length - 1) {
                    offetIndex++;
                    action();
                }
            });
        };
        action();
    }

    // Pulse
    function animation_pulse(elem) {
        var scaleIndex = 0;
        var scaleList = [1.1, 1];
        var action = function action() {
            animation.transition(elem, {
                styles: {
                    transform: 'scale(' + scaleList[scaleIndex] + ', ' + scaleList[scaleIndex] + ')'
                },
                duration: 500, //ms
                timingFunction: 'ease-in-out'
            }, function() {
                if (scaleIndex < scaleList.length - 1) {
                    scaleIndex++;
                    action();
                }
            });
        };
        action();
    }

    // Bounce
    function animation_bounce(elem) {
        var actionIndex = 0;
        var offetList = [0, -30, -30, 0, -15, 0, -4, 0];
        var durationList = [180, 200, 50, 100, 170, 100, 100, 100];
        var timingList = [
            'cubic-bezier(0.215, 0.61, 0.355, 1)',
            'cubic-bezier(0.755, 0.05, 0.855, 0.06)',
            'cubic-bezier(0.215, 0.61, 0.355, 1)',
            'cubic-bezier(0.755, 0.05, 0.855, 0.06)',
            'cubic-bezier(0.755, 0.05, 0.855, 0.06)',
            'cubic-bezier(0.215, 0.61, 0.355, 1)',
            'ease',
            'cubic-bezier(0.215, 0.61, 0.355, 1)'
        ];
        var action = function action() {
            animation.transition(elem, {
                styles: {
                    transform: 'translateY(' + offetList[actionIndex] + 'px)'
                },
                duration: durationList[actionIndex], //ms
                timingFunction: timingList[actionIndex]
            }, function() {
                if (actionIndex < offetList.length - 1) {
                    actionIndex++;
                    action();
                }
            });
        };
        action();
    }

    // Rubberband
    function animation_rubberband(elem) {
        var actionIndex = 0;
        var scaleXList = [1.25, 0.75, 1.15, 0.95, 1.05, 1];
        var scaleYList = [0.75, 1.25, 0.85, 1.05, 0.95, 1];
        var durationList = [300, 100, 100, 150, 100, 150];
        var action = function action() {
            animation.transition(elem, {
                styles: {
                    transform: 'scale(' + scaleXList[actionIndex] + ', ' + scaleYList[actionIndex] + ')'
                },
                duration: durationList[actionIndex], //ms
                timingFunction: 'ease-in-out'
            }, function() {
                if (actionIndex < scaleXList.length - 1) {
                    actionIndex++;
                    action();
                }
            });
        };
        action();
    }

    // Swing
    function animation_swing(elem) {
        var degIndex = 0;
        var degList = [15, -10, 5, -5, 0];
        var action = function action() {
            animation.transition(elem, {
                styles: {
                    transformOrigin: 'top',
                    transform: 'rotate(' + degList[degIndex] + 'deg)'
                },
                duration: 200, //ms
                timingFunction: 'ease-in-out'
            }, function() {
                if (degIndex < degList.length - 1) {
                    degIndex++;
                    action();
                }
            });
        };
        action();
    }

    // Tada
    function animation_tada(elem) {
        var degIndex = 0;
        var scaleList = [0.9, 0.9, 1.1, 1.1, 1.1, 1.1, 1.1, 1.1, 1.1, 1];
        var degList = [-3, -3, 3, -3, 3, -3, 3, -3, 3, 0];
        var action = function action() {
            animation.transition(elem, {
                styles: {
                    transformOrigin: 'top',
                    transform: 'rotate(' + degList[degIndex] + 'deg) scale(' + scaleList[degIndex] + ', ' + scaleList[degIndex] + ')'
                },
                duration: 100, //ms
                timingFunction: 'ease-in-out'
            }, function() {
                if (degIndex < degList.length - 1) {
                    degIndex++;
                    action();
                }
            });
        };
        action();
    }

    // BounceIn
    function animation_bounce_in(elem) {
        var degIndex = 0;
        var scaleList = [0.3, 1.1, 0.9, 1.03, 0.97, 1];
        var opList = [0, 1, 1, 1, 1, 1];
        var durationList = [0, 250, 250, 250, 250];
        var action = function action() {
            animation.transition(elem, {
                styles: {
                    opacity: opList[degIndex],
                    transformOrigin: 'top',
                    transform: 'scale(' + scaleList[degIndex] + ', ' + scaleList[degIndex] + ')'
                },
                duration: durationList[degIndex], //ms
                timingFunction: 'cubic-bezier(0.215, 0.61, 0.355, 1)'
            }, function() {
                if (degIndex < scaleList.length - 1) {
                    degIndex++;
                    action();
                }
            });
        };
        action();
    }

    // BounceOut
    function animation_bounce_out(elem) {
        var degIndex = 0;
        var scaleList = [0.9, 1.1, 1.1, 0.3, 1];
        var opList = [1, 1, 1, 0, 1];
        var durationList = [200, 250, 100, 450, 0];
        var action = function action() {
            animation.transition(elem, {
                styles: {
                    opacity: opList[degIndex],
                    transformOrigin: 'top',
                    transform: 'scale(' + scaleList[degIndex] + ', ' + scaleList[degIndex] + ')'
                },
                duration: durationList[degIndex], //ms
                timingFunction: 'cubic-bezier(0.215, 0.61, 0.355, 1)'
            }, function() {
                if (degIndex < scaleList.length - 1) {
                    degIndex++;
                    action();
                }
            });
        };
        action();
    }

    // ZoomIn
    function animation_zoom_in(elem) {
        var degIndex = 0;
        var scaleList = [0.3, 1];
        var opList = [0, 1];
        var durationList = [0, 500];
        var action = function action() {
            animation.transition(elem, {
                styles: {
                    opacity: opList[degIndex],
                    transformOrigin: 'top',
                    transform: 'scale(' + scaleList[degIndex] + ', ' + scaleList[degIndex] + ')'
                },
                duration: durationList[degIndex], //ms
                timingFunction: 'ease'
            }, function() {
                if (degIndex < scaleList.length - 1) {
                    degIndex++;
                    action();
                }
            });
        };
        action();
    }

    // ZoomOut
    function animation_zoom_out(elem) {
        var degIndex = 0;
        var scaleList = [0.3, 0.3, 1];
        var opList = [0, 0, 1];
        var durationList = [500, 500, 0];
        var action = function action() {
            animation.transition(elem, {
                styles: {
                    opacity: opList[degIndex],
                    transformOrigin: 'top',
                    transform: 'scale(' + scaleList[degIndex] + ', ' + scaleList[degIndex] + ')'
                },
                duration: durationList[degIndex], //ms
                timingFunction: 'ease'
            }, function() {
                if (degIndex < scaleList.length - 1) {
                    degIndex++;
                    action();
                }
            });
        };
        action();
    }

    export default {
        components : {WxcRadio},
        created () {
            var _this = this;
            setTimeout(function() {
                animation_base(_this.$refs.target_bg);
            }, 1000);
        },
        data() {
            return {
                // anim_data: {
                //     list: [
                //         {name: 'Flash', value: 1},
                //         {name: 'Shake', value: 2},
                //         {name: 'Pulse', value: 3},
                //         {name: 'Bounce', value: 4},
                //         {name: 'Rubberband', value: 5},
                //         {name: 'Swing', value: 6}
                //     ],
                //     defaultValue: { name: 'Flash', value: 1},
                //     displayValue (item) {
                //         return item.name;
                //     }
                // },
                anim_list: [
                    {title: 'Flash', value: 1},
                    {title: 'Shake', value: 2},
                    {title: 'Pulse', value: 3},
                    {title: 'Bounce', value: 4},
                    {title: 'Rubberband', value: 5},
                    {title: 'Swing', value: 6},
                    {title: 'Tada', value: 7},
                    {title: 'BounceIn', value: 8},
                    {title: 'BounceOut', value: 9},
                    {title: 'ZoomIn', value: 10},
                    {title: 'ZoomOut', value: 11},
                ],
            }
        },
        methods: {
            // handleChange() {
            //
            // },
            wxcRadioListChecked(e) {
                var _this = this;
                switch (e.value) {
                    case 1:
                        animation_flash(_this.$refs.target);
                        break;
                    case 2:
                        animation_shake(_this.$refs.target);
                        break;
                    case 3:
                        animation_pulse(_this.$refs.target);
                        break;
                    case 4:
                        animation_bounce(_this.$refs.target);
                        break;
                    case 5:
                        animation_rubberband(_this.$refs.target);
                        break;
                    case 6:
                        animation_swing(_this.$refs.target);
                        break;
                    case 7:
                        animation_tada(_this.$refs.target);
                        break;
                    case 8:
                        animation_bounce_in(_this.$refs.target);
                        break;
                    case 9:
                        animation_bounce_out(_this.$refs.target);
                        break;
                    case 10:
                        animation_zoom_in(_this.$refs.target);
                        break;
                    case 11:
                        animation_zoom_out(_this.$refs.target);
                        break;
                }
            }
        }
    }
</script>

<style scoped>
    .box {
        width: 250px;
        height: 250px;
        background-color: #DDD;
    }
    .target_bg {
        background-color: #feab3a;
        width: 750px;
        height: 200px;
        align-items: center;
        justify-content: center;
    }
    .target {
        color: white;
        font-size: 64px;
    }
    .split {
        background-color: #eee;
        font-size: 26px;
        height: 60px;
        padding-left: 24px;
        line-height: 60px;
        color: #666;
        width: 750px;
    }
</style>