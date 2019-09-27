<template>
    <div>
        <div class="group center">
            <div class="panel"><text class="text">{{value}}</text></div>
        </div>
        <div class="group">
            <mpwx-btn class="btn" label='Pick 一级' id="0" @onBtnClicked="pick"></mpwx-btn>
            <mpwx-btn class="btn" label='Pick 二级' id="3" @onBtnClicked="pick2"></mpwx-btn>
            <mpwx-btn class="btn" label='Pick 三级' id="4" @onBtnClicked="pick3"></mpwx-btn>
            <mpwx-btn class="btn" label='Pick Date' id="1" @onBtnClicked="pickDate"></mpwx-btn>
            <mpwx-btn class="btn" label='Pick Time' id="2" @onBtnClicked="pickTime"></mpwx-btn>
        </div>
    </div>
</template>

<script>
    const picker = weex.requireModule('picker');

    const items1 = ['广东', '湖南', '广西'];
    const items2 = [
        ['广州', '佛山', '东莞', '珠海'],
        ['长沙', '岳阳', '株洲', '衡阳'],
        ['桂林', '玉林']
    ];
    const items3 = [
        [
            ['白云区', '从化区', '海珠区', '花都区', '黄埔区', '荔湾区', '番禺区'],
            ['高明区', '南海区', '三水区', '顺德区'],
            ['茶山镇', '长安镇', '常平镇'],
            ['香洲区', '斗门区', '金湾区', '其它区']
        ],
        [
            ['芙蓉区', '开福区', '天心区', '雨花区', '岳麓区', '望城区', '长沙县'],
            ['君山区', '华容县', '岳阳楼区', '云溪区'],
            ['荷塘区', '芦淞区', '石峰区', '天元区', '株洲县'],
            ['石鼓区', '雁峰区', '蒸湘区', '珠晖区', '南岳区']
        ],
        [
            ['叠彩区', '临桂区', '七星区', '象山区', '秀峰区'],
            ['福绵区', '玉州区', '容县']
        ],
    ];

    function cValue(_this) {
        var ret = "";
        if (_this.index1 < items1.length && _this.index1 >= 0) {
            ret = items1[_this.index1] + " ";
            if (_this.index2 < items2[_this.index1].length && _this.index2 >= 0) {
                ret += items2[_this.index1][_this.index2] + " ";
                if (_this.index3 < items3[_this.index1][_this.index2].length && _this.index3 >= 0) {
                    ret += items3[_this.index1][_this.index2][_this.index3] + " ";
                }
            }
        }
        ret = ret.replace(/^\s+|\s+$/gm,'');
        if(ret.length < 1) {
            return '---';
        }else {
            return ret;
        }
    }

    import MpwxBtn from "../mpwx-btn"
    export default {
        components : {MpwxBtn},
        data () {
            return {
                value: '---',
                index1: -1,
                index2: -1,
                index3: -1,
            }
        },
        methods: {

            pick () {
                picker.pick({
                    index1: this.index1,
                    index2: -1,
                    index3: -1,
                    items1: items1,
                    title: "Picker Title"
                }, event => {
                    if (event.result === 'success') {
                        this.index1 = event.data1;
                        this.index2 = -1;
                        this.index3 = -1;
                        this.value = cValue(this);
                    }
                })
            },
            pick2 () {
                picker.pick({
                    index1: this.index1,
                    index2: this.index2,
                    index3: -1,
                    items1: items1,
                    items2: items2,
                    title: "Picker Title"
                }, event => {
                    if (event.result === 'success') {
                        this.index1 = event.data1;
                        this.index2 = event.data2;
                        this.index3 = -1;
                        this.value = cValue(this);
                    }
                })
            },
            pick3 () {
                picker.pick({
                    index1: this.index1,
                    index2: this.index2,
                    index3: this.index3,
                    items1: items1,
                    items2: items2,
                    items3: items3,
                    title: "Picker Title"
                }, event => {
                    if (event.result === 'success') {
                        this.index1 = event.data1;
                        this.index2 = event.data2;
                        this.index3 = event.data3;
                        this.value = cValue(this);
                    }
                })
            },
            pickTime () {
                picker.pickTime({
                    value: "09:30:01",
                    title: "Picker Title"
                }, event => {
                    if (event.result === 'success') {
                        this.value = event.data
                    }
                })
            },
            pickDate () {
                picker.pickDate({
                    value: "2017-01-22",
                    max: '2029-11-28',
                    min: '2005-11-28',
                    title: "Picker Title"
                }, event => {
                    if (event.result === 'success') {
                        this.value = event.data
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