<template>
    <div class="elem"
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
</style>