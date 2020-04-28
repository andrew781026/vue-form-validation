<template>
    <div>
        <p>By default, the width and height of an element is calculated like this:</p>
        <p>width + padding + border = actual width of an element</p>
        <p>height + padding + border = actual height of an element</p>
        <p> This means: When you set the width/height of an element, the element often appears bigger than you have set
            (because the element's border and padding are added to the element's specified width/height).</p>
        <p>The following illustration shows two &lt;div&gt; elements with the same specified width and height:</p>

        <div class="box-sizing">
            This div has exactly width = 500px and height = 100px
        </div>
        <div class="no-box">
            This div is bigger <br><br>
            width = 610px = 500px + 50px * 2 ( padding ) + 5px * 2 ( border ) <br><br>
            height = 210px = 100px + 50px * 2 ( padding ) + 5px * 2 ( border ) <br><br>
        </div>
    </div>

</template>

<script>
    export default {
        name: "BoxSizing"
    }
</script>

<style scoped>

    p {
        font-weight: 700;
    }

    /* 教學 : https://www.w3schools.com/css/css3_box-sizing.asp */
    .box-sizing {
        width: 500px;
        height: 100px;
        padding: 20px;
        margin: 20px;
        border: 5px solid blue;
        box-sizing: border-box;
    }

    .no-box {
        width: 500px;
        height: 100px;
        padding: 50px;
        border: 5px solid red;
    }
</style>
