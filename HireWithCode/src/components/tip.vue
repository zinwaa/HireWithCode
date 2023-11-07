<template>
    <div class="tip">已完成</div>
</template>


<script setup>
import { onMounted } from 'vue';
import $ from 'jquery'
onMounted(() => {
    
    console.log($(".tip")[0]);
})
</script>


<style scoped>
.tip {
    position: fixed;
    z-index: 10;
    background-color: white;
    font-size: 1rem;
    font-weight: 400;
    color: rgba(0, 119, 255, 0.918);
    top: 0;
}
.activity {
    animation: in-out 3s;
}

@keyframes in-out {
    from,
    to {
        opacity: 0;
        display: none;
    }

    10%,
    90% {
        opacity: 1;
    }
}
</style>