<template>
    <div>
        <div class="group center">
            <div class="panel"><text class="text">{{value}}</text></div>
        </div>
        <div class="group">
            <mpwx-btn class="btn" label='Pick 省(自治区、直辖市)' id="0" @onBtnClicked="pickProvince"></mpwx-btn>
            <mpwx-btn class="btn" label='Pick 市' id="1" @onBtnClicked="pickCity"></mpwx-btn>
            <mpwx-btn class="btn" label='Pick 区县' id="2" @onBtnClicked="pickDistrict"></mpwx-btn>
            <mpwx-btn class="btn" label='Pick 乡镇(街道)' id="3" @onBtnClicked="pickTown"></mpwx-btn>
        </div>
    </div>
</template>

<script>
    const areaPicker = weex.requireModule('areapicker');

    import MpwxBtn from "../mpwx-btn"
    export default {
        components : {MpwxBtn},
        data () {
            return {
                value: '---',
                province: '',
                city: '',
                district: '',
                town: '',
            }
        },
        methods: {
            pickProvince () {
                areaPicker.pickProvince({
                    province: this.province,
                    title: "请选择所在地区"
                }, event => {
                    if (event.result === 'success') {
                        this.province = event.data1;
                        this.value = this.province;
                    }
                })
            },
            pickCity () {
                areaPicker.pickCity({
                    province: this.province,
                    city: this.city,
                    title: "请选择所在地区"
                }, event => {
                    if (event.result === 'success') {
                        this.province = event.data1;
                        this.city = event.data2;
                        this.value = this.province + " " + this.city;
                    }
                })
            },
            pickDistrict () {
                areaPicker.pickDistrict({
                    province: this.province,
                    city: this.city,
                    district: this.district,
                    title: "请选择所在地区"
                }, event => {
                    if (event.result === 'success') {
                        this.province = event.data1;
                        this.city = event.data2;
                        this.district = event.data3;
                        this.value = this.province + " " + this.city + " " + this.district;
                    }
                })
            },
            pickTown () {
                areaPicker.pickTown({
                    province: this.province,
                    city: this.city,
                    district: this.district,
                    town: this.town,
                    title: "请选择所在地区"
                }, event => {
                    if (event.result === 'success') {
                        this.province = event.data1;
                        this.city = event.data2;
                        this.district = event.data3;
                        this.town = event.data4;
                        this.value = this.province + " " + this.city + " " + this.district + " " + this.town;
                    }
                })
            }
        }
    }
</script>

<style scoped>
    .panel {
        height: 200px;
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