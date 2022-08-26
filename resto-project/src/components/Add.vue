<template>
    <HeaderVue />
    <h1>Welcome to add employee page</h1>
    <form class="add">
        <h3>Add Employee</h3>
        <h6>Its quick and easy</h6>
        <input v-model="name" type="text" placeholder="Enter name" name="name">
        <input v-model="role" type="text" placeholder="Enter role" name="role">
        <input v-model="salary" type="number" placeholder="Enter salary" name="salary">
        <input v-model="contact" type="number" placeholder="Enter contact" name="contact">
        <button type="button" @click="addEmployee">Add Employee</button>
        <h4 v-show="emptyFields">Please provide all details!!!</h4>
        <h1 v-show="addSuccess" class="face">Employee added!!!</h1>
    </form>

</template>

<script>
import HeaderVue from './Header.vue';
import axios from 'axios';

export default {
    name: 'AddResto',
    data() {
        return {
            name: '',
            role: '',
            salary: '',
            contact: '',
            emptyFields: false,
            addSuccess: false
        }
    },
    components: {
        HeaderVue
    },
    methods: {
        async addEmployee() {

            if (this.name == '' || this.role == '' || this.salary == '' || this.contact == '') {
                this.emptyFields = true;
                console.log('Please provide all details');
            } else {
                const result = await axios.post("http://localhost:3000/Employees",
                    {
                        name: this.name,
                        role: this.role,
                        salary: this.salary,
                        contact: this.contact
                    }
                );
                if (result.status == 201) {
                    this.name = '', this.role = '', this.salary = '', this.contact = '', this.addSuccess = true,
                        setTimeout(() => {
                            this.$router.push({ name: 'Home' })
                        }, 2000);
                }
            }
            // alert("Button working")
        }
    }
    // mounted() {
    //     let user = localStorage.getItem('Users-Info');
    //     if (!user) {
    //         this.$router.push({ name: "LoginPage" })
    //     }
    // }
}
</script>

<style scoped>
h3 {
    text-align: center;
    width: 100%;
    margin: 31px 0 0 0;
}

.face {
    color: rgb(0, 174, 0);
    animation: shake 2s cubic-bezier(.9, .9, .9, .97) both;
    transform: translate3d(0, 0, 0);
    backface-visibility: hidden;
    perspective: 1000px;
}

@keyframes shake {

    10%,
    90% {
        transform: translate3d(-20px, 0, 0);
    }

    20%,
    80% {
        transform: translate3d(20px, 0, 0);
    }

    30%,
    50%,
    70% {
        transform: translate3d(-20px, 0, 0);
    }

    40%,
    60% {
        transform: translate3d(20px, 0, 0);
    }
}
</style>