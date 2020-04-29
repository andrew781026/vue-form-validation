<template>
    <div id="app">
        <div style="margin: 20px">
            <GridForm/>
        </div>
    </div>
</template>

<script>
    import GridForm from './components/GridForm.vue'

    export default {
        name: 'App',
        components: {
            GridForm,
        }
    }
</script>

<style>


    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        color: #2c3e50;
    }
</style>
