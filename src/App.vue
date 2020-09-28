<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <div id="app" class="small-container">
    <h1>Employees</h1>
    <employee-form v-on:add:employee="addEmployee"/>
    <employee-table 
      v-bind:employees="availableEmployees"
      v-on:delete:employee="deleteEmployee"
      v-on:edit:employee="editEmployee"
    />

  </div>
</template>

<script>
import EmployeeTable from './components/EmployeeTable.vue'
import EmployeeForm from './components/EmployeeForm.vue'
import availableEmployees from './data/employees'

export default {
  name: 'App',
  components: {
    EmployeeForm,
    EmployeeTable,
  },
  data() {
    return {
      availableEmployees
    }
  },
  methods: {
    addEmployee(employee) {
      const lastId = 
        this.availableEmployees.length > 0
        ? this.availableEmployees[this.availableEmployees.length - 1].id
        : 0
      
      const id = lastId + 1
      const newEmployee = { ...employee, id }

      this.availableEmployees = [...this.availableEmployees, newEmployee]
    },
    deleteEmployee(id) {
      this.availableEmployees = this.availableEmployees.filter( employee => id !== employee.id )
    },
    editEmployee(id, updatedEmployee) {
      this.availableEmployees = this.availableEmployees.map(employee =>
        employee.id === id ? updatedEmployee : employee
      )
    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
