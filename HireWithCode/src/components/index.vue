<template>
    <div class="index markdown-body" v-html="context"></div>
    <div v-show="acceptChallenge" class="acceptChallenge" @click.stop="close1">
        <form action="" @click.stop="" @submit.prevent="commit1">
            <div>
                <label for="githubID">Github ID</label>
                <inputBox type="text" id="githubID" v-model="githubID" />
            </div>
            <div>
                <label for="email">邮箱</label>
                <inputBox type="text" id="email" v-model="email" />
            </div>
            <button type="commit">提交</button>
        </form>
    </div>
    <div v-show="successesChallenge" class="successesChallenge" @click.stop="close2">
        <form action="" @click.stop="" @submit.prevent="commit2">
            <div>
                <label for="githubUrl">Github url</label>
                <inputBox type="text" id="githubUrl" v-model="githubUrl" />
            </div>
            <div>
                <label for="url">在线体验地址</label>
                <inputBox type="text" id="url" v-model="url" />
            </div>
            <button type="commit">提交</button>
        </form>
    </div>
    <div class="tip">
        {{ tipText }}
    </div>
</template>


<script setup>
import $ from 'jquery'
import { onMounted, ref } from 'vue';
import { marked } from 'marked'
import "github-markdown-css"
import inputBox from './inputbox.vue'
const text = `# HireWithCode - 面试者挑战项目

欢迎来到 \`HireWithCode\` 项目！这是一个专为技术面试者设计的真实项目挑战。目前，这个仓库刚刚起步，没有任何代码——只有待实现的功能（TODOs）。你的任务是将这些TODOs转变为实际的代码，提交你的Pull Request（PR）就是你面试的一部分挑战。

## 产品功能 TODOs
产品是一个 Web 网站（PC端、移动端兼容），分为 4 个步骤的页面：
- [ ] **欢迎语**：Logo + 一句话欢迎语（垂直水平居中，2 秒后自动进入下一页 *面试引导*）\`欢迎来到 Onedigi 线上面试环节，期待你的加入！\` [logo](./logo.png) 
- [ ] **面试引导**：介绍面试的流程和说明（Markdown 文案展示，需要渲染为富文本样式）[页面文案 markdown](https://raw.githubusercontent.com/onedigi/HireWithCode/main/README.md)
- [ ] **接受挑战**：表单，\`input\`(用户输入自己的 github id) 、\`input\`(邮箱)、\`submit button\`(接受挑战)
- [ ] **完成挑战**：表单，\`input\`(github 仓库 url)、\`input\`([Vercel](https://vercel.app/) 在线体验地址)、\`submit button\`(提交作品)

## 如何参与？

1. 克隆仓库到你的本地机器。
2. 按照你对这个产品的理解，自行开发 TODO
4. 确保你的代码是可以运行的
5. 完成挑战后，通过Pull Request将你的代码提交给我们。
6. 在PR中附上你的Vercel在线体验链接。

> 备注说明：
> 这个项目的步骤 3、4 是是需要服务端能力的（API + 数据库），如果你不具备全栈的经验，可以考虑使用 [supabase](https://supabase.com/) 作为本项目的服务端（或者仅仅实现前端静态网页）

我们会审查每一个PR，并以此作为面试的一部分。我们期待看到你的创意和技术实力！

祝你好运！`
const context = marked(text)
const acceptChallenge = ref(false)
const successesChallenge = ref(false)
const close1 = () => {
    acceptChallenge.value = false
    $("[type = checkbox]")[2].checked = false
    // console.log($("[type = checkbox]")[2].checked);
}
const close2 = () => {
    successesChallenge.value = false
    $("[type = checkbox]")[3].checked = false
    console.log($("[type = checkbox]")[3].checked);
}
const tipText = ref("")
const commit1 = () => {
    let tipDom = document.getElementsByClassName("tip")[0]
    if (githubID.value !== "" && email.value !== "") {
        tipText.value = "已提交，已打印在控制台"
        console.log("Github ID:", githubID.value);
        console.log("email:", email.value);
        acceptChallenge.value = false
        $("[type = checkbox]")[2].checked = true
        $("[type = checkbox]")[2].disabled = true
        $("[type = checkbox]")[3].disabled = false
        tipDom.classList.add("ojbk")
        setTimeout(() => tipout("ojbk"), 2000)
    }
    else {
        $("[type = checkbox]")[2].checked = false
        tipText.value = "表单不能为空"
        tipDom.classList.add("no")
        setTimeout(() => tipout("no"), 2000)
    }
}
const commit2 = () => {
    let tipDom = document.getElementsByClassName("tip")[0]
    if (githubUrl.value !== "" && url.value !== "") {
        tipText.value = "已提交，已打印在控制台"
        console.log("Github Url:", githubUrl.value);
        console.log("url:", url.value);
        successesChallenge.value = false
        $("[type = checkbox]")[3].disabled = true
        tipDom.classList.add("ojbk")
        setTimeout(() => tipout("ojbk"), 2000)
    }
    else {
        $("[type = checkbox]")[3].checked = false
        tipText.value = "表单不能为空"
        tipDom.classList.add("no")
        setTimeout(() => tipout("no"), 2000)
    }
}
const tipout = (tip) => {
    let tipDom = document.getElementsByClassName("tip")[0]
    tipDom.classList.remove(tip)
}
onMounted(() => {
    $("[type = checkbox]")[0].disabled = false
    $("[type = checkbox]")[1].disabled = false
    $("[type = checkbox]")[2].disabled = false

    setTimeout(() => {
        $("[type = checkbox]")[0].checked = true
        setTimeout(() => { $("[type = checkbox]")[0].disabled = true }, 500)
    }, 3500)
    setTimeout(() => {
        $("[type = checkbox]")[1].checked = true
        setTimeout(() => { $("[type = checkbox]")[1].disabled = true }, 500)
    }, 4000)

    $("[type = checkbox]")[2].onchange = () => {
        acceptChallenge.value = true
    }
    $("[type = checkbox]")[3].onchange = () => {
        successesChallenge.value = true
    }
})

</script>


<style scoped>
.tip {
    position: fixed;
    top: 9vh;
    text-align: center;
    transition: all 0.25s ease-in-out;
    opacity: 0;
    z-index: 20;
    padding: 0.8vh 1.8vw;
    background-color: white;
    text-align: center;
    border-radius: 4px;
    font-size: 0.9rem;
}
.ojbk{
    border: 1px solid rgb(39, 139, 253);
    box-shadow: 1px 0 4px 1px rgb(160, 204, 255), -1px 0 4px 1px rgb(160, 204, 255);
    color: rgb(39, 139, 253);
    transform: translateX(30vw);
    opacity: 1;
}
.no{
    border: 1px solid rgb(255, 74, 74);
    box-shadow: 1px 0 4px 1px rgb(255, 146, 146), -1px 0 4px 1px rgb(255, 146, 146);
    color: rgb(255, 74, 74);
    transform: translateX(40vw);
    opacity: 1;
}

.index {
    padding: 5vw;
}

label::after {
    content: " :";
}

.acceptChallenge,.successesChallenge {
    position: fixed;
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: white;
    top: 0;
    left: 0;
}

.acceptChallenge:focus-visible,.successesChallenge:focus-visible {
    outline: none;
}

form {
    display: flex;
    gap: 1.5vh;
    flex-direction: column;
    padding: 4vh 2vw;
    border-radius: 4px;
    box-shadow: 2px 0 8px 8px #ccc;
    width: 85%;
}

@media(min-width: 768px) {
    form {
        width: 38vw;
    }
    .ojbk{
        transform: translateX(40vw);
    }
    .no{
        transform: translateX(45vw);
    }
}

form div {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    gap: 10px;
}

label {
    font-size: 0.9rem;
    color: rgba(0, 0, 0, 0.95);
}

button {
    background: white;
    border: 1px solid rgb(39, 139, 253);
    color: rgb(39, 139, 253);
    border-radius: 4px;
    width: 80%;
    margin-left: 10%;
    margin-top: 5%;
    cursor: pointer;
    transition: all 0.3s;
}

button:focus-visible {
    outline: none;
}

button:hover {
    color: white;
    background-color: rgb(39, 139, 253);
}

.finish {
    animation: out 1s;
}

@keyframes out {
    100% {
        transform: translateX(20px);
        opacity: 0;
    }
}
</style>