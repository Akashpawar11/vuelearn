<template>
    <HeaderVue />
    <h1>Welcome to home page</h1>
    <h2>List Of Employees</h2>

    <table>
        <tr id="headTr">
            <th>ID</th>
            <th>Name</th>
            <th>Role</th>
            <th>Salary</th>
            <th>Contact</th>
            <th>Actions</th>
        </tr>
        <tr v-for="item in employees" :key="item.id">
            <td id="idTd">{{ item.id }}</td>
            <td id="nameTd">{{ item.name }}</td>
            <td>{{ item.role }}</td>
            <td>{{ item.salary }}</td>
            <td>{{ item.contact }}</td>
            <td class="actionsTd">
                <router-link :to="/update/ + item.id">
                    <span id="editIcon" class='fas'>&#xf044;</span>
                </router-link>
                <span @click="removeData(item.id)" id="removeIcon" class='fas'>&#xf1f8;</span>
            </td>
        </tr>
    </table>
</template>

<script>
import HeaderVue from './Header.vue';
import axios from 'axios';

export default {
    name: 'HomePage',
    data() {
        return {
            employees: []
        }
    },
    components: {
        HeaderVue
    },
    async mounted() {
        let user = localStorage.getItem('Users-Info');
        if (!user) {
            this.$router.push({ name: "LoginPage" })
        }
        let result = await axios.get("http://localhost:3000/Employees");
        console.table(result.data)
        this.employees = result.data
    },
    methods: {
        async removeData(id) {
            console.warn(id)
            let result = await axios.delete("http://localhost:3000/Employees/" + id);
            if (result.status == 200) {
                this.$router.push({ name: "LoginPage" })
            }
        }
    }
}
</script>

<style scoped>
table {
    width: 60%;
    margin-left: auto;
    margin-right: auto;
}

table,
td,
th {
    border: 1px solid white;
    border-collapse: collapse;
    background-color: #00000047;

}

td,
th {
    padding: 10px;
}

#headTr {
    color: rgb(255 221 0 / 98%);
    background-color: #f3f3f37d;

}

#idTd {
    background-color: rgb(0 174 0 / 22%);
}

#nameTd {
    background-color: rgb(255 40 40 / 22%);
}

a {
    text-decoration: none;
}

.actionsTd {
    padding: 0px;
}

#editIcon {
    width: 37%;
    color: transparent;
    text-align: center;
    text-shadow: 0 0 0 #21cb21;
}

#removeIcon {
    cursor: pointer;
    width: 37%;
    text-align: center;
    font-size: 15px;
    color: red;
    /* height: 20px;
    width:20px; */
}
</style>