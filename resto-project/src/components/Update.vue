<template>
    <HeaderVue />
    <h1>Update Employee details page</h1>
    <form class="update">
        <h3>Update Employee details</h3>
        <input v-model="name" type="text" placeholder="Enter name" name="name">
        <input v-model="role" type="text" placeholder="Enter role" name="role">
        <input v-model="salary" type="number" placeholder="Enter salary" name="salary">
        <input v-model="contact" type="number" placeholder="Enter contact number" name="contact">
        <button type="button" @click="updateEmployee">Update Employee</button>
        <h4 v-show="emptyFields">Please provide all details!!!</h4>
        <h3 v-show="addSuccess">Employee data updated!!!</h3>
    </form>

</template>

<script>
import HeaderVue from './Header.vue';
import axios from 'axios'

export default {
    name: 'UpdateEmployee',
    data() {
        return {
            name: '',
            role: '',
            contact: '',
            salary: '',
            emptyFields: false,  //if any of the input fields is empty
            addSuccess: false    //shows success message after successful update
        }
    },
    components: {
        HeaderVue
    },
    async mounted() {
        let user = localStorage.getItem('Users-Info');
        if (!user) {
            this.$router.push({ name: "LoginPage" }); //if user not logged in route to login page
        }
        console.warn(this.$route.params.id);  
        let result = await axios.get("http://localhost:3000/employees/" + this.$route.params.id); //return data of selected element
        this.name = result.data.name;             //updates input fields with fetched details from api
        this.role = result.data.role;
        this.salary = result.data.salary;
        this.contact = result.data.contact;
    },
    methods: {
        async updateEmployee() {
            let result1 = await axios.put("http://localhost:3000/employees/" + this.$route.params.id,
                {
                    name: this.name,
                    role: this.role,
                    salary: this.salary,
                    contact: this.contact
                }
            );
            if (result1.status == 200) {
                this.addSuccess = true;
                setTimeout(() => {
                    this.$router.push({ name: 'Home' })
                }, 2000);
            }
        }
    }
}

</script>

<style scoped>
h3 {
    /* margin-left: auto; */
    /* margin-right: auto; */
    text-align: center;
    width: 70%;
    margin: 30px auto;
}
</style>