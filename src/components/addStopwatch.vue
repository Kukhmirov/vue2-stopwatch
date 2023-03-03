<template>
    <div class="addstopwatch">
        <button class="btnsvg">
            <svg class="plus" width="20" height="20" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
                <path d="M20 10L0 10" stroke-width="3"></path>
                <path d="M10 20L10 0" stroke-width="3"></path>
            </svg>
        </button>
    </div>
</template>

<script>
export default {
    name: 'addStopwatch',
}
</script>


<style>
.plus {
    stroke: #9e9e9e;
}
.btnsvg {
    border: none;
    background: none;
}
.addstopwatch {
    background-color: #696969;
    width: 225px;
    height: 180px;
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 25px;
}
.addstopwatch:hover {
    cursor: pointer
}
.addstopwatch:hover .plus {
    stroke: #fff;
}
</style>