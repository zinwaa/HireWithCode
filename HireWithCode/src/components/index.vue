<template>
    <div class="index markdown-body" v-html="context"></div>
    <div tabindex="1" v-if="acceptChallenge" class="acceptChallenge" @click.stop="">
        <form action="">
            <div>
                <label for="githubID">Github ID</label>
                <input type="text" id="githubID">
            </div>
            <div>
                <label for="githubID">邮箱</label>
                <inputBox />
                <input type="text" id="githubID">
            </div>
            <button type="button">提交</button>
        </form>
    </div>
    <div tabindex="2" v-if="false">
        <form action=""></form>
    </div>
</template>


<script setup>
import $ from 'jquery'
import { onMounted, reactive, ref } from 'vue';
import { marked } from 'marked'
import "github-markdown-css"
import inputBox from './inputBox.vue'
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
const acceptChallenge = ref(true)
onMounted(() => {
    $("[type = checkbox]")[0].disabled = false
    $("[type = checkbox]")[1].disabled = false
    $("[type = checkbox]")[2].disabled = false

    setTimeout(() => {
        $("[type = checkbox]")[0].checked = true
        
    }, 3500)
    setTimeout(() => {
        $("[type = checkbox]")[1].checked = true
    }, 4000)

    const isChallenge = ref(false)
    const challengeChange = () => {
        isChallenge.value = !isChallenge.value
    }
    $("[type = checkbox]")[2].onchange = () => {
        challengeChange
        acceptChallenge.value= true
    }
})

</script>


<style scoped>
.index {
    padding: 5vw;
}
label::after {
    content: " :";
}
.acceptChallenge {
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
.acceptChallenge:focus-visible {
    outline: none;
}
form {
    display: flex;
    gap: 1.5vh;
    flex-direction: column;
    padding: 4vh 2vw;
    border-radius: 4px;
    box-shadow: 2px 0 8px 8px #ccc;
    
}
form div{
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    gap: 10px;
}
label {
    font-size: 0.9rem;
}
button {
    background: white;
    border:1px solid rgb(39, 139, 253);
    color: rgb(39, 139, 253);
    border-radius: 4px;
    width: 80%;
    margin-left:10% ;
    margin-top: 5%;
    cursor: pointer;
}
</style>