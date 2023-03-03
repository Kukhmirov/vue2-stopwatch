<template>
    <div id="app">
        <container />
    </div>
</template>

<script>
import container from './components/container'

export default {
    name: 'App',
    components: {
        container,
    },
}
</script>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
button:hover {
    cursor: pointer;
}
</style>
