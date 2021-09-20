<template>
  <div id="app">
    <h1>New branch</h1>
    <h1 class="text-4xl font-bold">User Data</h1>
    <button class="px-4 py-2 mt-10 font-bold text-white bg-blue-500 rounded hover:bg-blue-700" @click="visible=true">Add User</button>
    <modal :isVisible="visible"  @cancel="visible = false" @confirm="saveUser"></modal>
    <custom-table :msg="users"></custom-table>
  </div>
</template>

<script>
import CustomTable from './components/Table.vue'
import Modal from './components/modal.vue'

export default {
  name: 'App',
  data() {
   return {
    users: [
      { name: 'Hira', email: 'hira@gmail.com',phone:'123',address:'lahore',country:'Pakistan' },
      { name: 'Maryam', email: 'maryam@gmail.com',phone:'234',address:'lahore',country:'Pakistan' }
    ],
    visible: false
   }
  },
  components: {
    CustomTable,
    Modal
  },
  methods: {
    saveUser: function(user){
      this.users.push({
        name: user.name,
        email: user.email,
        phone: user.phone,
        address: user.address,
        country: user.country
      });

      this.visible=false;
      user.name=""
      user.email=''
      user.phone=''
      user.address=''
      user.country=''
    }
  }
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
