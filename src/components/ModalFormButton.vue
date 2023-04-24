<script lang="ts">
import {} from 'vue';

export default ({

    props: {
        btnName: String,
        btnClass: String,
        formTitle: String,
        formType: Boolean,
        testfun: {
            type: Function,
            required: true
        }
    },

    setup() {

        return {

        }
    }
})
</script>

<template>
<h1> This is Button Component</h1>
<button class="new_employee_btn" @click="testfun()">click me</button>

<!-- Button -->
<!-- <v-row justify="center">
            <v-dialog v-model="insertForm" persistent width="600">
                <template v-slot:activator="{ props }">
                    <v-btn @click="insertForm = true" variant="outlined" :class=btnClass v-bind="props">{{ btnName }}</v-btn>
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
    </v-row> -->
</template>

<style scoped>
.new_employee_btn {
    background-color: rgb(150, 192, 211);
    border: 2px solid black;
    border-radius: 5px;
    color: black;
    transition: all 0.2s ease-in-out;
}

.new_employee_btn:hover {
    background-color: black;
    color: rgba(150, 192, 211, 0.877);
}

.delete_btn {
    width: 60px;
    height: 36px;
    border: 2px solid rgb(143, 143, 143);
    border-radius: 3px;
    padding: 2px;
    color: black;
    transition: all 0.2s ease-in-out;
}

.delete_btn:hover {
    background-color: #a51000;
    color: white;
    cursor: pointer;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
}

.edit_btn {
    width: 55px;
    border: 2px solid rgb(43, 41, 41);
    border-radius: 3px;
    padding: 2px;
    color: black;
    font-family: sans-serif;
}

.edit_btn:hover {
    background-color: #02854f;
    color: white;
    cursor: pointer;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
}
</style>
