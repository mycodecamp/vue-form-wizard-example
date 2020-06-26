<template>
  <div id="app">
    <div v-if="submitted" class="alert_box">
      <div class="alert alert-success" role="alert">Your form has been submitted</div>
    </div>              
 
    <div v-else>    
      <form-wizard @on-complete="onComplete" shape="square" color="#3498db">
        <h1 slot="title">Registration Form</h1> 

        <tab-content title="Application Form" icon="ti-user" :before-change="()=>validate()">
          <div class="application-form" id="step-1" ref="Application">
                                  
            <div class="form-group row">
              <div class="col-sm">Name:</div>
              <div class="col-sm">
                <input class="form-control" placeholder="Full Name*" name="fullname" v-model="fullname" :class="{ 'is-invalid': $v.fullname.$error }" />
                <div v-if="!$v.fullname.required" class="invalid-feedback">Full name is required</div>
              </div>                          
            </div>
            <div class="form-group row">
              <div class="col-sm">Address:</div>
              <div class="col-sm">
                <textarea class="form-control" placeholder="Address" name="address" v-model="address" :class="{ 'is-invalid': $v.address.$error }"></textarea>
                <div v-if="!$v.address.required" class="invalid-feedback">Address is required</div>
              </div>                          
            </div>
            <div class="form-group row">
              <div class="col-sm">Age:</div>
              <div class="col-sm">
                <input class="form-control" placeholder="Age" name="age" v-model="age"  maxlength="3" type="number" :class="{ 'is-invalid': $v.age.$error }" />
                <div v-if="!$v.age.required" class="invalid-feedback">Age is required</div>
              </div>                          
            </div>
            <div class="form-group row">
              <div class="col-sm">Email:</div>
              <div class="col-sm">
                <input class="form-control" placeholder="Email" name="email" v-model="email"  type="email" :class="{ 'is-invalid': $v.email.$error }" />
                <div v-if="$v.email.$error" class="invalid-feedback">
                  <span v-if="!$v.email.required">Email is required</span>
                  <span v-else-if="!$v.email.refemail">Email is invalid</span>
                </div>   
              </div>                          
            </div>
            
          </div>
        </tab-content>

        <tab-content title="Preview" icon="ti-eye" >
          <div class="preview-form" id="step-2">
                                  
            <div class="form-group row">
              <div class="col-sm">Name:</div>
              <div class="col-sm">{{fullname}}</div>
            </div>
            <div class="form-group row">
              <div class="col-sm">Address:</div>
              <div class="col-sm">{{address}}</div>
            </div>
            <div class="form-group row">
              <div class="col-sm">Age:</div>
              <div class="col-sm">{{age}}</div>                          
            </div>
            <div class="form-group row">
              <div class="col-sm">Email:</div>
              <div class="col-sm">{{email}}</div>
            </div>
           
          </div>
        </tab-content>

        <tab-content title="Conformation & Apply" icon="ti-check" >
          <p>Click <strong>finish</strong> to completed the process</p>
        </tab-content>
      </form-wizard>
    </div>
  </div>
</template>
<style>
.form-group >:first-child{
  font-weight: bold;
}
</style>

<script>
import { required, email} from 'vuelidate/lib/validators'
import '@/assets/css/themify-icons/themify-icons.css'

export default {
  name: 'App',
  data() {
    return {
      fullname:'',
      address:'',
      age:'',
      email:'',
      submitted:false
      
    }
  },
  validations: {
    fullname: { required},
    address: { required},
    age: { required},
    email: { required, email },
  },
  methods: {
    validateStep(name) {
          var refToValidate = this.$refs[name]; 
          console.log(refToValidate)           
          return refToValidate.validate();
    },
    onComplete: function(){    
      this.submitted=true
    },
    validate() {
      this.$v.$touch()      
      var isValid = !this.$v.$invalid
      return isValid
    }
  }
}
</script>

<style>
#app {
  width:50%;
  margin:auto;
}
</style>
