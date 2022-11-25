<template>
    <div class="register_page">
        <img class="logo_login" src="../assets/logobanhpia-trang.jpg" alt="">
        <h1>Đăng Ký</h1>

        <input type="text" v-model="name" placeholder="Vui Lòng Nhập Tên">
        <input type="email" v-model="email" placeholder="Vui Lòng Nhập Email">
        <input type="password" v-model="password" placeholder="Vui Lòng Nhập Mật Khẩu">
        <button v-on:click="signUp">Đăng Ký</button>
        <p>
            Bạn đã có tài khoản
            <router-link to="/login">
                Đăng Nhập
            </router-link>
        </p>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    name: 'RegisterPage',
    data() {
        return {
            name: '',
            email: '',
            password: ''
        }
    },
    methods: {
        async signUp() {
            let result = await axios.post("http://localhost:3000/users", {
                email: this.email,
                password: this.password,
                name: this.name
            });

            console.warn(result);
            if (result.status == 201) {
                localStorage.setItem("user-info", JSON.stringify(result.data))
                this.$router.push({ name: 'HomePage' })
            }
        }
    },
    mounted() {
        let user = localStorage.getItem('user-info');
        if (user) {
            this.$router.push({ name: 'HomePage' })
        }
    }
}
</script>

<style>
.logo_login {
    width: 300px;
}

.register_page p {
    margin: 30px 0px 20px 50px;
}

.register_page h1 {
    margin: 30px 0px 20px 80px;
}

.register_page input {
    width: 320px;
    height: 40px;
    padding-left: 20px;
    margin-bottom: 30px;
    border: 1px solid #ccc;
    display: block;
}

.register_page button {
    font-size: 18px;
    width: 320px;
    height: 40px;
    border: 1px solid skyblue;
    background: skyblue;
    color: #fff;
    cursor: pointer;
    border-radius: 20px;
}
</style>