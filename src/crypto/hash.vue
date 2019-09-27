<template>
    <div class="wrapper">
        <text class="text">{{defText}}</text>
    </div>
</template>

<script>
    const crypto = weex.requireModule("crypto");
    module.exports = {
        data: {
            defText: ''
        },
        created() {
            const rawD = new Uint8Array(['a', 'b', 'c']);

            crypto.hash({
                type: 'md5',
                content: ['a', 'b', 'c']
            }, (e) => {
                const {result, data = '', message = ''} = e;
                if(result == 'success') {
                    this.defText = data;
                }
            });
        }
    }
</script>

<style scoped>
    .wrapper {
        justify-content: center;
        align-items: center;
        padding: 20px;
    }
    .text {
        font-size: 20px;
    }
</style>