<template>
    <div class="elem"
         v-bind:class="{active: isActive}"
         @click="isActive = !isActive"
    >{{elem.name}}</div>
</template>
<script>
export default {
    name: 'ElementList',
    props: {
        elem: {
            type: Object,
            requered: true,
        }
    },
    data (){
        return{
            isActive: false
        }
    }
}
</script>
<style>
    .elem{
        border: 1px solid !important;
        width: 100%;
    }
    .elem:hover{
        background-color: red;
        color: white;
    }
    .active{
        background-color: red;
        color: white;
    }
</style>