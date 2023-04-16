<script lang="ts">
import { defineComponent, ref, onMounted } from 'vue';
import axios from 'axios';


type Employee = {
  id: number;
  first_name: string;
  last_name: string;
  email: string;
  phone: string;
  salary : number;
  departmentId : number
}


export default defineComponent({
  name: 'Employee',
  setup() {
    const employees = ref([]);
    var dialog = ref(false)


    // variables for getting data from input form
    var first_name = ref("")
    var last_name = ref("")
    var email = ref("")
    var phone = ref("")
    var salary = ref("")
    var departmentId = ref("") 
    
    

    // Insert new employee
    const addEmployee = async () => {

      // send form data to API
      try
      {
        const data = {
        firstname: first_name.value,
        lastname: last_name.value,
        email: email.value,
        phone : phone.value,
        salary: salary.value,
        departmentId: departmentId.value
      }

      const response = await axios.post('http://localhost:5240/api/Employee/Insert_Employee', data)

      console.log(response)

        first_name.value = ""
        last_name.value= ""
        email.value = ""
        phone.value = ""
        salary.value = ""
        departmentId.value = "" 

        alert("Employee Inserted Successfully")

        dialog.value = false;

      }

      catch(error)
      {
        console.log(error)
        alert("Input All  the details first")
      }
      
    }


     // Delete an employee by id
     const deleteEmployee = async (id: number) => {
      await axios.delete(`http://localhost:5240/api/Employee/Delete Employee/${id}`);
      alert("Employee Deleted Successfully");
      // Remove the deleted employee from the employees array
      employees.value = employees.value.filter((employee) => employee.id !== id);
    };


    onMounted(async () => {
      const response = await axios.get('http://localhost:5240/api/Employee');
      employees.value = response.data;
    });

    return { 
      employees,
      dialog,
      first_name,
      last_name,
      email,
      phone,
      salary,
      departmentId,
      addEmployee,
      deleteEmployee,
    };
  },
});
</script>




<template>
    <div class="table-name">
        <h2>All Employee Details</h2>
        <!-- Insert new employee -->
        <v-row justify="center">
    <v-dialog v-model="dialog" persistent width="700">
      <template v-slot:activator="{ props }">
        <v-btn @click="dialog = true" class="new_employee_btn" v-bind="props">+ New Employee</v-btn>
      </template>
      <v-card>
        <v-card-title>
          <span class="text-h5">Insert Employee Details</span>
        </v-card-title>
        <v-card-text>
          <v-container>
            <v-row>
              <v-col cols="12" sm="6" md="4">
                <v-text-field label="First name*" required v-model="first_name"></v-text-field>
              </v-col>
              <v-col cols="12" sm="6" md="4">
                <v-text-field label="Last name*" required v-model="last_name"></v-text-field>
              </v-col>
              <v-col cols="12">
                <v-text-field label="Email*" required v-model="email"></v-text-field>
              </v-col>
              <v-col cols="12">
                <v-text-field label="Phone*" required v-model="phone"></v-text-field>
              </v-col>
              <v-col cols="12" sm="5">
                <v-text-field label="Salary*" type="number" required v-model="salary"></v-text-field>
              </v-col>
              <v-col cols="12" sm="3">
                <v-text-field label="Department*" type="number" required v-model="departmentId"></v-text-field>
              </v-col>
            </v-row>
          </v-container>
          <small>*indicates required field</small>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn class="delete_btn" variant="text" @click="dialog = false"> Close </v-btn>
          <v-btn class="edit_btn" variant="text" @click="addEmployee"> Save </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-row>
    </div>
  <table class="table">
    <thead>
        
        <hr><hr>
        <br>
        <br>
        <br>
      <tr>
        <th style="width: 100px;" class="th">ID</th>
        <th class="th">First Name</th>
        <th class="th">Last Name</th>
        <th class="th">Email</th>
        <th class="th">Phone</th>
        <th class="th">Salary</th>
        <th class="th">Department Name</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="employee in employees" :key="employee.id">
        <!-- <td> Id </td> -->
        <td>{{ employee.id }}</td>
        <td>{{ employee.firstName }}</td>
        <td>{{ employee.lastName }}</td>
        <td>{{ employee.email }}</td>
        <td>{{ employee.phone }}</td>
        <td>{{ employee.salary }}</td>
        <td>{{ employee.departmentName }}</td>
        <td>
            <button class="edit_btn">Edit</button>
        </td>
        <td>
            <Button class="delete_btn" @click="deleteEmployee(employee.id)">Delete</Button></td>
      </tr>
    </tbody>
  </table>
</template>
  
  

<style scoped>

.table-name{
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-top: 150px;
    margin-left: 100px;
}

.table-name h2{
    background-color: black;
    color: whitesmoke;;
    width: 250px;
}

.table .th{
    background-color: rgb(183, 196, 191);
}
.new_employee_btn{
    background-color: black;
    color: white ;
    transition: all 0.2s ease-in-out;
}

.new_employee_btn:hover{
    background-color: black;
    color: aquamarine;
}

.table {
  border-collapse: collapse;
  width: 85%;
  font-weight: 16px;
  margin-left: 100px;
  
}

.newbtn{
    background-color: black;
    color: white;
    height: 30px;
    transition: all 0.2s ease-in-out;
}

.newbtn:hover{
    background-color: black;
    color: aqua;
    height: 30px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
}


.delete_btn{
    width: 55px;
    border: 1px solid rgb(143, 143, 143);
    border-radius: 3px;
    padding: 2px;
    color: black;
}
.delete_btn:hover{
    background-color: #a51000;
    color: white;
    cursor: pointer;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
}

.edit_btn{
    width: 55px;
    border: 1px solid rgb(143, 143, 143);
    border-radius: 3px;
    padding: 2px;
    color: black;
}

.edit_btn:hover{
    background-color: #02854f;
    color: white;
    cursor: pointer;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
}

thead h1{
    background-color: aquamarine;
    width: 100;
}

.table th,
.table td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: left;
}

.table th {
  background-color: #f2f2f2;
  color: #333;
}

.table tr:nth-child(even) {
  background-color: #f2f2f296;
}

</style>