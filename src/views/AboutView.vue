<script lang="ts">
import { defineComponent, ref } from 'vue'

export default defineComponent({
  setup() {
    let edit_employee = ref(false)

    return {
      edit_employee
    }
  }
})
</script>

<template>
  <div class="about">
    <h1>This is an about page</h1>
  </div>
  <br>
  <v-row justify="center">
    <v-dialog v-model="edit_employee" persistent width="700">
      <template v-slot:activator="{ props }">
        <v-btn @click="edit_employee = true"  class="edit_btn"  text v-bind="props">Edit</v-btn>
      </template>
      <v-card>
        <v-card-title>
          <span class="text-h5">Update Employee Details</span>
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
              <v-col cols="12" sm="3">
                <v-text-field label="Salary*" type="number" required></v-text-field>
              </v-col>
            </v-row>
          </v-container>
          <small>*indicates required field</small>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="blue-darken-1" variant="text" @click="edit_employee = false"> Close </v-btn>
          <v-btn color="blue-darken-1" variant="text" @click="edit_employee = false"> Save </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-row>

</template>

<style scoped>

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

.about {
  margin-top: 150px;
}
</style>
