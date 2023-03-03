<template>
    <div class="container">
        <theStopwatch
            v-for="i in countStopwatches"
            :key="i"
        />
        <div @click="add">
            <addStopwatch/>
        </div>
    </div>
</template>

<script>
import theStopwatch from './theStopwatch';
import addStopwatch from './addStopwatch';

export default {
    name: 'TheContainer',
    data() {
        return {
            countStopwatches: 2
        };
    },
    components: {
        theStopwatch,
        addStopwatch,
    },
    methods: {
        add() {
            this.countStopwatches++
        },
    },
}
</script>

<style>
.container {
    width: 100%;
    margin: auto;
    margin-top: 47px;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
}
</style>