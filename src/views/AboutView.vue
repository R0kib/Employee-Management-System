<template>
<div class="about">
    <h1>This is an about page</h1>

    <!-- <ModalFormButton 
    btn-name="+ Add Employee" 
    btn-class="new_employee_btn" 
    form-title="Insert Employee Details" 
    :testfun="testFun" /> -->

    <br><br>
    <hr><br>

    <!-- <ModalFormButton 
      btn-name="Edit"
      btn-class="edit_btn"
      form-title="Update Employee Details"
      :testfun="myfun"
    /> -->
</div>
<br>
</template>



<script lang="ts">
import {
    defineComponent,
    ref
} from 'vue'
import ModalFormButton from '@/components/ModalFormButton.vue';
export default defineComponent({
    setup() {

        const modal = ref(true)

        const testFun = () => {
            console.log("This is Parent class function");
            console.log(modal.value);
            modal.value = false;
            console.log(modal.value);
            
        }

        return {
            testFun
        };

    },
    components: {
        ModalFormButton
    }
})
</script>



<style scoped>
.about {
    margin-top: 150px;
    margin-left: 40px;
}
</style>
