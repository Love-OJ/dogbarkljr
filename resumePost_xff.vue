<template>
    <div class="container">
        <h1 class="header">OJ简历投递啦！</h1>

        <!--<p>只要你有一颗想要学习的心！</p>-->

        <form @submit.prevent="submitForm">
            <label for="name">姓名：</label>
            <input type="text" id="name" v-model="formData.name" name="name" placeholder="请输入姓名" required>

            <label for="id">学号：</label>
            <input type="text" id="id" name="id" v-model="formData.id" placeholder="请输入学号" required>

            <label for="class">班级：</label>
            <input type="text" id="class" name="class" v-model="formData.class" placeholder="请输入班级" required>

            <label for="school">高中母校：</label>
            <input type="text" id="school" name="school" v-model="formData.school" placeholder="请输入高中母校" required>

            <label for="englishScore">高考英语成绩：</label>
            <input type="number" id="englishScore" v-model="formData.englishScore" name="englishScore"
                placeholder="请输入高考英语成绩" required>

            <label for="gender">性别：</label>
            <select id="gender" v-model="formData.gender" name="gender" required>
                <option value="">请选择性别</option>
                <option value="male">男</option>
                <option value="female">女</option>
            </select>

            <label for="dob">出生日期：</label>
            <input type="date" id="dob" v-model="formData.dob" name="dob" required>

            <label for="phone">联系电话：</label>
            <input type="tel" id="phone" name="phone" v-model="formData.phone" placeholder="请输入联系电话" required>

            <label for="email">电子邮箱：</label>
            <input type="email" id="email" name="email" v-model="formData.email" placeholder="请输入电子邮箱" required>

            <label for="introduction">自我介绍：</label>
            <textarea id="introduction" v-model="formData.introduction" name="introduction" placeholder="请简要介绍自己"
                rows="4" required></textarea>

            <label for="joinStudentUnion">是否加入学生会：</label>
            <select id="joinStudentUnion" v-model="formData.joinStudentUnion" @change="toggleStudentUnionFields"
                name="joinStudentUnion" required>
                <option value="">请选择</option>
                <option value="yes">是</option>
                <option value="no">否</option>
            </select>
            <div id="studentUnionFields" v-if="formData.joinStudentUnion == 'yes'">
                <label for="studentUnionName">加入的学生会：</label>
                <input type="text" id="studentUnionName" v-model="formData.studentUnionName" name="studentUnionName"
                    placeholder="请输入加入的学生会名称">

                <label for="mainTasks">主要任务：</label>
                <textarea id="mainTasks" v-model="formData.mainTasks" name="mainTasks" placeholder="请简要描述主要任务"
                    rows="4"></textarea>
            </div>

            <button type="submit">提交</button>
        </form>
    </div>
</template>

<script>
import axios from 'axios'; // 导入 axios

export default {
    name: 'App',
    formData:{},
    data() {
        return {
            formData: {
                'name': '',
                'id': '',
                'class': '',
                'school': '',
                'englishScore': '',
                'gender': '',
                'dob': '',
                'phone': '',
                'mail': '',
                'introduction': '',
                'joinStudentUnion': '',
                'studentUnionName': '',
                'mainTasks':'',
            }
        };
    },
    methods: {
        toggleStudentUnionFields() {
            // 这个方法在选择是否加入学生会时会被调用
        },
        async submitForm() {
            try {
                // 将表单数据转换为 JSON 格式
                const response = await axios.post('http://127.0.0.1:5000/submit',this.formData)
                .then(response=>{
                    console.log('success post',response.data)
                })
                .catch(error=>{
                    console.log('Error',error)
                })
                console.log(this.formData)
                if (response.status === 200) {
                    alert('提交成功！'); // 提交成功后显示返回的消息
                   
                } else {
                    alert('提交失败，请重试。');
                }
            } catch (error) {
                console.error('Error:', error);
                alert('提交过程中发生错误，请重试。');
            }
        }

    },
    
}
</script>

<style>
/* 你的样式代码保持不变 */
body {
    background-image: url('../back.gif');
    background-size: cover;
    background-position: center;
    font-family: Arial, sans-serif;
    margin: 100;
    height: 100vh;
    justify-content: center;
    align-items: center;
}

.container {
    background-color: rgba(0, 0, 0, 0.7);
    padding: 100px;
    border-radius: 10px;
    box-shadow: 0 40px 20px rgba(0, 0, 0, 0.5);
    color: white;
    margin: 20px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    text-align: center;
}

label {
    display: block;
    margin: 10px 0 5px;
}

input,
select,
textarea {
    width: 100%;
    padding: 10px;
    margin-bottom: 10px;
    border: 1px solid #ccc;
    border-radius: 4px;
}

button {
    padding: 10px 15px;
    background-color: #28a745;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    width: 100%;
}

button:hover {
    background-color: #218838;
}

.hidden {
    display: none;
}
</style>