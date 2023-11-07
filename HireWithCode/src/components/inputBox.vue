<template>
    <input type="" autocomplete="off">
</template>

<script>
export default {
    setup(){
    },
    mounted(){
    }
}
</script>
<style scoped>
input {
    width: 65%;
    display: inline-block;
    border: 1px solid #ccc;
    transition: all 0.3s;
    padding: 2px 10px;
    border-radius: 2px;
    font-size: 14px;
}
input:hover {
    border: 1px solid rgb(39, 139, 253);
}
input:focus-visible {
    outline: none;
    border: 1px solid rgb(39, 139, 253);
    box-shadow: 1px 0 4px 1px rgb(160, 204, 255), -1px 0 4px 1px rgb(160, 204, 255);
}

</style>