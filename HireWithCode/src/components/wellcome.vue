<template>
    <div class="wellcome">
        <img src="./icons/logo.png">
        <span>欢迎来到 Onedigi 线上面试环节，期待你的加入！</span>
    </div>
</template>


<script setup>
import $ from 'jquery'
import { onMounted } from 'vue';
onMounted(() => {
    const doms = {
        wellcome: $(".wellcome")[0]
    }
    setTimeout(() => doms.wellcome.style.display = "none", 2500)
})

</script>


<style scoped>
.wellcome {
    position: fixed;
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    animation: in-out 3s;
    z-index: 10;
    background-color: white;
}

@keyframes in-out {

    from,
    to {
        opacity: 0;
        display: none;
    }

    10%,
    90% {
        display: flex;
        opacity: 1;
    }
}

.wellcome img {
    width: 3vw;
    height: 3vw;
}

.wellcome span {
    font-size: 3vw;
    margin-left: 1vw;
}

@media(max-width:768px) {
    .wellcome span {
        font-size: 3vh;
        margin-left: 1vh;
    }

    .wellcome img {
        width: 3vh;
        height: 3vh;
    }
}</style>