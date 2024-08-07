<script setup>
import { ref } from "vue";
const employeeDetail = ref(null);
const isLoggedIn = ref(false);
const employee = ref(["Karan Kumar","Shravan Kumar","Suresh Kumar"]);

const handleAddEmployee = () => {
  let empName = employeeDetail.value;
  if(empName.length !== 0 && isLoggedIn) employee.value.push(empName);

}

const handleLogin = () => {
  isLoggedIn.value = !isLoggedIn.value;
}

const handleDeleteTask = (id) => {
  employee.value.splice(id,1);
}

</script>

<template>
  <button @click="handleLogin" v-if="isLoggedIn">Logout</button>
  <button @click="handleLogin" v-else>Login</button>
  <div>


    <div v-if="isLoggedIn">
      <form @submit.prevent="handleAddEmployee">
        <label>
          <input type="text" v-model="employeeDetail" />
        </label>
        <button type="submit">Add</button>
      </form>
      <h2>Employee Details</h2>
      <ul v-for="(emp,id) in employee">
        <li :id="id">
          {{ emp }}
          <button @click="handleDeleteTask(id)">Delete</button>
        </li>
      </ul>
    </div>
    <div v-else class="notify-msg">Employee Data Only shown to logged in user. kindly logged in</div>

  </div>

</template>

<style scoped>
* {
  margin: 0;
}

.notify-msg{
  color: red;
  font-size: 1.5rem;
  font-weight: bold;
  margin: 1rem 0;
}
</style>
