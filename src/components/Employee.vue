<script lang="ts">
import { defineComponent, ref, onMounted } from 'vue';
import axios from 'axios';


interface Employee {
  id: number,
  name: string,
  department: string,
  email: string,
  phone: string
}


export default defineComponent({
  name: 'Employee',
  setup() {
    const employees = ref([]);
    const dialog = ref(false)

    onMounted(async () => {
      const response = await axios.get('http://localhost:5240/api/Employee');
      employees.value = response.data;
    });

    return { 
      employees,
      dialog
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
                <v-text-field label="First name*" required></v-text-field>
              </v-col>
              <v-col cols="12" sm="6" md="4">
                <v-text-field
                  label="Last name*"
                ></v-text-field>
              </v-col>
              <v-col cols="12">
                <v-text-field label="Email*" required></v-text-field>
              </v-col>
              <v-col cols="12">
                <v-text-field label="Phone*" required></v-text-field>
              </v-col>
              <v-col cols="12" sm="5">
                <v-text-field label="Salary*" type="number" required></v-text-field>
              </v-col>
              <v-col cols="12" sm="3">
                <v-text-field label="Department*" type="number" required></v-text-field>
              </v-col>
            </v-row>
          </v-container>
          <small>*indicates required field</small>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="blue-darken-1" variant="text" @click="dialog = false"> Close </v-btn>
          <v-btn color="blue-darken-1" variant="text" @click="dialog = false"> Save </v-btn>
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
      <tr v-for="  employee in employees" :key="employee.id">
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
            <Button class="delete_btn">Delete</Button></td>
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