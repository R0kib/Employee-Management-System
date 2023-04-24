<script lang="ts">
import { defineComponent, ref } from 'vue';
import axios from 'axios';



export default defineComponent({
  name: 'Employee',
  setup() {
    const employees = ref([]);
    var insertForm = ref(false);
    var updateForm = ref(false);

    var update_emp_id : any;
    

    // variables for details of employee
    var first_name = ref("")
    var last_name = ref("")
    var email = ref("")
    var phone = ref("")
    var salary = ref("")
    var departmentId = ref("") 

    // var employee = ref(
    //     [
    //         first_name = ref(""),
    //         last_name = ref(""),
    //         email = ref(""),
    //         phone = ref(""),
    //         salary = ref(""),
    //         departmentId = ref("") 
    //     ]
    // )
    

    var departments = [
      { dept_name: "HR",dept_id: 1  },
      {  dept_name: "Developer" ,dept_id: 2 },
      { dept_name: "Tester" ,dept_id: 3}
    ];
    
    // show all employees
    const fetchEmployees =async () => {
        const response = await axios.get('http://localhost:5240/api/Employee');
        employees.value = response.data;
    }
    
    fetchEmployees();



    // Insert new employee
    const addEmployee = async () => 
    {
    

        try
        {
            const data = {
                firstname: first_name.value,
                lastname: last_name.value,
                email: email.value,
                phone : phone.value,
                salary: salary.value,
                departmentId: departmentId.value,       
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

            insertForm.value = false;

            fetchEmployees();

        }

        catch(error)
        {
            console.log(error)
            alert("Input All  the details first")
        }
      
    }







    //get employee details in the form
    const showUpdateForm = async (employee: any) => 
    {   
        update_emp_id = employee.id;
        first_name.value = employee.firstName;
        last_name.value = employee.lastName;
        email.value = employee.email;
        phone.value = employee.phone;
        salary.value = employee.salary;
        departmentId.value = employee.departmentName;
        updateForm.value = true;

        console.log(employee);
    }


    // clear the form
    const clearForm = () => 
    {   
        first_name.value = "";
        last_name.value = "";
        email.value = "";
        phone.value = "";
        salary.value = "";
        departmentId.value = "";
        updateForm.value = false;
        insertForm.value = false;

    }


    // update employee details
    const updateEmployee = async () =>
    {  
        try
        {
            const data = {
            id : update_emp_id,
            firstname: first_name.value,
            lastname: last_name.value,
            email: email.value,
            phone : phone.value,
            salary: salary.value,
            departmentId: departmentId.value,       
            }
            console.log("data",data)


           const response = await axios.put('http://localhost:5240/api/Employee/Update_Employee', data)

           console.log(response)


            clearForm();
            alert("Employee Updated Successfully")

           fetchEmployees();

        }

        catch(error)
        {
            console.log(error)
            alert("Input All  the details first")
        }

            

    }

     // Delete an employee by id
     const deleteEmployee = async (id: number) => {


        if(confirm("Are you sure you want to delete this employee?"))
        {

            console.log("Delete Id =" + id);
            try
        {
            await axios.delete(`http://localhost:5240/api/Employee/Delete_Employee?empId=`+id);

            fetchEmployees();
            alert("Employee Deleted Successfully");

        }
      
            catch(error)
            {
                console.log(error);
                alert("Error Occurred" + id);
            }
        }

        
    };


    


    return { 
      employees,
      insertForm,
      updateForm,
      first_name,
      last_name,
      email,
      phone,
      salary,
      departmentId,
      fetchEmployees,
      addEmployee,
      updateEmployee,
      deleteEmployee,
      showUpdateForm,
      clearForm,
      departments,
    };
  },
});
</script>




<template>
    <div class="table-name">
        <h2>All Employee Details</h2>

        <!-- Insert new employee -->
        <v-row justify="center">
            <v-dialog v-model="insertForm" persistent width="600">
                <template v-slot:activator="{ props }">
                    <v-btn @click="insertForm = true" variant="outlined" class="new_employee_btn" v-bind="props">+ Add Employee</v-btn>
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
                        <v-col cols="8">
                            <v-text-field label="Email*" required v-model="email"></v-text-field>
                        </v-col>
                        <v-col cols="8">
                            <v-text-field label="Phone*" required v-model="phone"></v-text-field>
                        </v-col>
                        <v-col cols="12" sm="5">
                            <v-text-field label="Salary*" type="number" required v-model="salary"></v-text-field>
                        </v-col>
                        <v-col cols="12" sm="5">
                            <v-autocomplete
                                v-model="departmentId"
                                :items=departments
                                item-title="dept_name"
                                item-value="dept_id"
                                label="Department"
                            ></v-autocomplete>
                        </v-col>
                        </v-row>
                    </v-container>
                    <small>*indicates required field</small>
                    </v-card-text>
                    <v-card-actions>
                    <v-spacer></v-spacer>
                    <v-btn class="delete_btn" variant="text" @click="clearForm"> Close </v-btn>
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
            <!-- Edit options -->
            <!-- <button class="edit_btn">Edit</button> -->
            <v-row justify="center">
                <v-dialog v-model="updateForm" persistent width="600">
                <template v-slot:activator="{ props }">
                    <v-btn class="edit_btn"  text v-bind="props" @click="showUpdateForm(employee)">Edit</v-btn>
                  
                </template>
                <v-card>
                    <v-card-title>
                    <span class="text-h5">Update Employee Details</span>
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
                        <v-col cols="8">
                            <v-text-field label="Email*" required v-model="email"></v-text-field>
                        </v-col>
                        <v-col cols="8">
                            <v-text-field label="Phone*" required v-model="phone"></v-text-field>
                        </v-col>
                        <v-col cols="12" sm="5">
                            <v-text-field label="Salary*" type="number" required v-model="salary"></v-text-field>
                        </v-col>
                        <v-col cols="12" sm="5">
                            <v-autocomplete
                                v-model="departmentId"
                                :items=departments
                                item-title="dept_name"
                                item-value="dept_id"
                                label="Department"
                            ></v-autocomplete>
                        </v-col>
                        </v-row>
                    </v-container>
                    <small>*indicates required field</small>
                    </v-card-text>
                    <v-card-actions>
                    <v-spacer></v-spacer>
                    <v-btn class="delete_btn" variant="text" @click="clearForm"> Close </v-btn>
                     <v-btn class="edit_btn" variant="text" @click="updateEmployee()"> Save </v-btn>
                    </v-card-actions>
                </v-card>
                </v-dialog>
            </v-row>
        </td>
        <td>
            <!-- Delete options -->
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
    background-color: rgb(150, 192, 211);
    border: 2px solid black;
    border-radius: 5px;
    color: black ;
    transition: all 0.2s ease-in-out;
}

.new_employee_btn:hover{
    background-color: black;
    color: rgba(150, 192, 211, 0.877);
}

.table {
  border-collapse: collapse;
  width: 85%;
  font-weight: 16px;
  margin-left: 100px;
  
}


.delete_btn{
    width: 60px;
    height: 36px;
    border: 1px solid rgb(143, 143, 143);
    border-radius: 3px;
    padding: 2px;
    color: black;
    transition: all 0.2s ease-in-out;
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
    font-family: sans-serif;
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