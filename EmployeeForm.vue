<template>
    <div id="employee-form">
        <form @submit.prevent="handleSubmit">
        <label>Employee name</label>
        <input type="text" v-model="employee.name"
        :class="{'has-error':submitting&&invalidName}"
        @focus="clearStatus"
        @keypress="clearStatus"
        />
        <br><br>
        <label >Employee Email</label>
        <input type="text" v-model="employee.email" 
        :class="{'has-error' :submitting&&invalidEmail}"
        @focus="clearStatus"
        @keypress="clearStatus"
        />
        <br><br>
        <label >Employee Firstname</label>
        <input type="text" v-model="employee.Firstname" 
        :class="{'has-error' :submitting&&invalidFirstname}"
        @focus="clearStatus"
        @keypress="clearStatus"
        />
        <br><br>
        <label >Employee Lastname</label>
        <input type="text" v-model="employee.Lastname"
        :class="{'has-error' :submitting&&invalidLastname}"
        @focus="clearStatus"
        @keypress="clearStatus"
        />
        <br><br><br>
        <button>Add Employee</button>
        </form>
    </div>
</template>
<script>
export default {
    name : 'employee-form',
    data(){
        return{
            submitting: false,
            success:false,
            error:false,
            employee:{
                name:'',
                email:''
            }
        }
    },
    methods:{
        handleSubmit(){
            this.submitting=true;
            this.clearStatus();
            if(this.invalidName||this.invalidEmail){
                this.error=true;
                return;
            }
            this.$emit('add:employee',this.employee);
            this.employee = {
                name:'',
                email:''
            };
            this.success=true;
            this.error=false;
            this.submitting=false;
        },
        clearStatus(){
            this.success=false;
            this.error=false;
        }
    },
    computed:{
        invalidName(){
            return this.employee.name==='';
        },
        invalidEmail(){
            return this.employee.email==='';
        }
    }
}
</script>
<style scoped>
     form{
        margin-bottom: 2rem;
     }
</style>