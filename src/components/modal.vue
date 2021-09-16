<template lang='pug'>
  div(v-if="isVisible")
    div.fixed.inset-0.z-50.flex.justify-center.items-center
      div.flex.flex-col.flex-1.max-w-xl.rounded-lg.shadow-lg.bg-white
        // header
        <div class="flex justify-between p-5 bg-blue-500 rounded-t">
             <h3 class="text-2xl font-semibold text-white">Add User</h3>
             <button class="p-1 leading-none text-white hover:bg-gray-600 hover:text-black" @click="emitCancel">
                <div class="w-6 h-6 text-xl font-semibold">
                    <span>x</span>
                </div>
             </button>
        </div>
    
        // body
        <form>
        <div class="p-6">
         <p v-if="errors.length">
          <b>Please correct the following error(s):</b>
        <ul>
          <li v-for="error in errors">{{ error }}</li>
        </ul>
        </p>
        
        <div class="flex flex-col justify-around mt-10 ">
            <span class="block mb-1 text-sm font-bold text-left text-gray-700 ">Username</span>
            <input class="px-3 py-2 leading-tight text-gray-700 border rounded shadow appearance-none focus:outline-none focus:shadow-outline" v-model="user.name" id="username" type="text" placeholder="Username">
            
            <label class="block mb-1 text-sm font-bold text-left text-gray-700 mt-7" for="email">Email</label>
            <input class="px-3 py-2 leading-tight text-gray-700 border rounded shadow appearance-none focus:outline-none focus:shadow-outline" v-model="user.email" id="email" type="text" placeholder="Email">
            
            <label class="block mb-1 text-sm font-bold text-left text-gray-700 mt-7" for="phone">Phone</label>
            <input class="px-3 py-2 leading-tight text-gray-700 border rounded shadow appearance-none focus:outline-none focus:shadow-outline" v-model="user.phone" id="phone" type="text" placeholder="Phone">
            
            <label class="block mb-1 text-sm font-bold text-left text-gray-700 mt-7" for="phone">Address</label>
            <input class="px-3 py-2 leading-tight text-gray-700 border rounded shadow appearance-none focus:outline-none focus:shadow-outline" v-model="user.address" id="address" type="text" placeholder="Address">
            
            <label class="block mb-1 text-sm font-bold text-left text-gray-700 mt-7" for="phone">Country</label>
            <country-select class="w-full px-3 py-2 border rounded shadow" v-model="user.country" :country="user.country" countryName="true" topCountry="US" />
            </div>
        </div>

        // footer
        <div class="flex items-end justify-end p-6">
        <button @click.prevent="emitCancel" class="px-4 py-2 font-semibold text-blue-700 bg-transparent border border-blue-500 rounded hover:bg-blue-500 hover:text-white hover:border-transparent">Cancel</button>
        <button @click.prevent="emitConfirm" class="px-4 py-2 mx-3 font-bold text-white bg-blue-500 border border-blue-700 rounded hover:bg-blue-700">Save</button>
        </div>
        </form>  
    div.opacity-25.fixed.inset-0.z-40.bg-black
</template>

<script>

import Vue from 'vue'
import vueCountryRegionSelect from 'vue-country-region-select'
Vue.use(vueCountryRegionSelect)


export default {
  name: 'Modal',
  props: {
    isVisible: Boolean
  },
  data:function() {
      return{
        errors: [],
        user: {
            name: '',
            email: '',
            phone: '',
            address: '',
            country: ''
        }
      }
  },
  components: {
       "vue-country-select": require("vue-country-select")
  },
  methods: {
      emitCancel() {
      console.log("cancel called")
      this.user.name=''
      this.user.email=''
      this.user.phone=''
      this.user.address=''
      this.user.country=''
      this.errors= []
      this.$emit('cancel');
    },
    emitConfirm() {
      console.log("emit called")
      console.log(this.user.name)
      console.log(this.user.email)
      console.log(this.user.phone)
      console.log(this.user.address)
      console.log(this.user.country)

      this.errors = [];

      if (!this.user.name) {
        this.errors.push("Name required.");
      }
      if (!this.user.email) {
        this.errors.push('Email required.');
      } else if (!this.validEmail(this.user.email)) {
        this.errors.push('Valid email required.');
      }

      if (!this.user.phone) {
        this.errors.push('Phone required.');
      }  else if (!this.validPhone(this.user.phone)) {
        this.errors.push('Valid phone required.');
      }

      if (!this.user.address) {
        this.errors.push('Address required.');
      } 

      if (this.errors.length==0) {
      this.$emit('confirm',this.user);
      }
    },
    
    validEmail: function (email) {
        
      var re = /^[\w]+@([\w-]+\.)+[\w-]{2,4}$/;
      return re.test(email);
    },
    validPhone: function (phone) {
        
      var re = /^\(?([0-9]{4})\)?[-. ]?([0-9]{7})$/;
      return re.test(phone);
    }
  }
}
</script>
