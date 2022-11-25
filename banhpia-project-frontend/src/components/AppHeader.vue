<template>
  <nav class="navbar navbar-expand navbar-dark bg-dark">
    <a href="/admin" class="navbar-brand" id="nav_admin"
      >Bánh Pía Đặc Sản Sóc Trăng</a
    >
    <div class="mr-auto navbar-nav">
      <li class="nav-item">
        <router-link to="/" class="nav-link"> Trang Chủ </router-link>
        <router-link to="/product" class="nav-link"> Sản Phẩm </router-link>
        <router-link to="/introduce" class="nav-link"> Giới Thiệu </router-link>
        <router-link to="/login" class="nav-link"> Đăng Nhập </router-link>
        <router-link to="/register" class="nav-link"> Đăng Ký </router-link>
        <a class="nav-link" v-on:click="logout" href="#">Đăng Xuất</a>
        <router-link to="/shopping_cart" class="nav-link">
          <i class="fas fa-cart-shopping"></i>
          Giỏ Hàng
        </router-link>
      </li>
    </div>
  </nav>
</template>

<script>
export default {
  data() {
    return {
      carts: [],
    };
  },
  methods: {
    logout() {
      localStorage.clear();
      this.$router.push({ name: "LoginPage" });
    },
  },
  mounted() {
    const listLoalCart = JSON.parse(localStorage.getItem("cart") ?? "[]");
    this.carts = listLoalCart;
  },
};
</script>

<style>
.navbar {
  top: 0;
}

.nav-link {
  float: left;
}

/* .navbar {
    margin-left: 181px;
    margin-right: 181px;
} */

#nav_admin {
  margin-right: 80px;
  margin-left: 181px;
}
</style>
