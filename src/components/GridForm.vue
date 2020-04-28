<template>
    <div :style="{width}">
        <div v-if="title" class="form-title">
            {{title}}
        </div>
        <div class="form-body">
            <div class="item" :key="n" v-for="n in 10">
                <div class="cell-title">{{String.fromCharCode(64+n)}}</div>
                <div class="cell-value">{{String.fromCharCode(944+n)}}</div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "GridForm",
        props: {
            width: {
                type: String,
                default: '70%'
            },
            title: {
                type: String,
                default: '表格 - 修改密碼'
            }
        },
    }
</script>

<style scoped>

    .form-title {
        height: 30px;
        padding: 10px;
        display: flex;
        align-items: center;
        border: 1px solid rgba(128, 137, 155, 0.5);
        font-weight: 900;
        font-size: 24px;
        color: #f0f8ff;
        background-color: #120dad;
    }

    /* 教學 : https://www.w3schools.com/css/css_grid_container.asp */
    .form-body {
        display: grid;
        grid-template-columns: 25% 25% 25% 25%; /* 4 column one row */
    }

    .item {
        border: 1px solid rgba(128, 137, 155, 0.3);
        display: flex;
        align-items: center;
    }

    .cell-title {
        background-color: #00ffff;
        padding: 10px;
        height: 100%;
        width: 60px;
        text-align: right;
    }

    .cell-value {
        padding: 10px;
        height: 100%;
    }
</style>
