<template>
    <div class="wrapper">
        <scroller class="sc" show-scrollbar="false">
            <mpwx-cell v-for="item in defList" :key="item.label"
                       :label="item.label"
                       :icon="item.icon"
                       :windowTitle="item.windowTitle"
                       :href="item.href">
            </mpwx-cell>
        </scroller>
    </div>
</template>

<script>
    import MpwxCell from "./mpwx-cell"
    module.exports = {
        components : {MpwxCell},
        data: {
            defList: [
                {label: "获取系统环境 (Environment)", icon: "", windowTitle: "Environment", href: "/demos/env.js"},
                {label: "关于 (About)", icon: "", windowTitle: "About", href: "/demos/about.js"},
            ]
        }
    }
</script>

<style scoped>
    .wrapper {
        justify-content: center;
        align-items: center;
    }
    .sc {
        width: 750px;
    }
</style>