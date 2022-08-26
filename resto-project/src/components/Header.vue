<template>
    <div class="nav">
        <!-- <img src="../assets/qq.png" height=50 width=50 alt=""> -->
        <router-link to="/">Home</router-link>
        <router-link to="/add">Add Employee</router-link>
        <router-link to="logoutBtn" @click="logout">Logout</router-link>
        <!-- <div class="fan">
            <div class="fanblade1"></div>
            <div class="fanblade2"></div>
        </div> -->
    </div>
</template>

<script>
export default {
    name: 'HeaderVue',
    methods: {
        logout() {
            localStorage.clear();
            // prompt("Do you really want to logout");
            this.$router.push({ name: 'LoginPage' })
        }
    }
}
</script>

<style>
/* .fan{
    display: inline-block;
    height: 100px;
    width: 100px;
    background-color: rgb(0, 0, 0);
}
.fanblade1{
    height: 100px;
    width: 10px;
    margin: 0px 44px;
    background-color: chocolate;
    transition-duration: 10s;
}
.fanblade2{
    height: 10px;
    width: 100px;
    margin: -50px 0px;
    background-color: chocolate;
    transition-duration: 10s;
}
.fanblade1:hover,.fanblade2:hover{
    transform: rotate(3400deg);
} */
.nav     {
    background-color: rgb(44, 43, 43);
    min-width: 540px;
    overflow: hidden;
}

.nav a {
    font-family: 'Montserrat', sans-serif;
    color: antiquewhite;
    padding: 15px 25px;
    text-decoration: none;
    float:left;
}

.nav a:hover {
    background-color: rgb(208, 208, 208);
    color: black;
}

.logoutBtn {
    float: right;
}

::-webkit-scrollbar {
    display: none;
}
</style>