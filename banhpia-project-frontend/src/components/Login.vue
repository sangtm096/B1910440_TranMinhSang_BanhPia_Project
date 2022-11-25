<template>
    <div class="login_page">
        <img class="logo_login" src="../assets/logobanhpia-trang.jpg" alt="">
        <h1>Đăng Nhập</h1>
    
        <input type="email" v-model="email" placeholder="Vui Lòng Nhập Email">
        <input type="password" v-model="password" placeholder="Vui Lòng Nhập Mật Khẩu">
        <button v-on:click="login">Đăng Nhập</button>
        <p>
            Bạn chưa có tài khoản
            <router-link to="/register">
                Đăng Ký
            </router-link>
        </p>
    </div>
</template>

<script>
import AppHeaderVue from './AppHeader.vue';
import axios from 'axios';
export default {
    name: 'LoginPage',
    components: {
        AppHeaderVue
    },
    data() {
        return {
            email: '',
            password: ''
        }
    },
    methods: {
        async login() {
            let result = await axios.get(
                `http://localhost:3000/users?email=${this.email}&password=${this.password}`
            )

            if (result.status == 200 && result.data.length > 0) {
                localStorage.setItem("user-info", JSON.stringify(result.data[0]))
                this.$router.push({ name: 'HomePage' })
            }
            console.warn(result)
        }
    },
    mounted() {
        let user = localStorage.getItem('user-info');
        if (user) {
            this.$router.push({ name: 'HomePage' })
        }
    }
};

</script>

<style>
.logo_login {
    width: 300px;
}

.login_page h1 , .login_page p {
    margin-left: 50px; 
    margin-bottom: 20px;
    margin-top: 30px;
}

.login_page input {
    width: 320px;
    height: 40px;
    padding-left: 20px;
    margin-bottom: 30px;
    border: 1px solid #ccc;
    display: block;
}

.login_page button {
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