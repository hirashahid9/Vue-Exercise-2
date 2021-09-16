<template>
  <div class="hello">
    <br>
    <table class="w-5/6 m-5 mx-auto text-gray-800 bg-gray-200 rounded-t-lg">
    <tr class="text-center border-b-2 border-gray-300">
        <th class="px-4 py-3">Name</th>
        <th class="px-4 py-3">Email</th>
        <th class="px-4 py-3">Phone</th>
        <th class="px-4 py-3">Address</th>
        <th class="px-4 py-3">Country</th>
    </tr>
    <tr  class="bg-gray-100 border-b border-gray-200" v-for="user in msg" :key="user.email">
        <td class="px-4 py-3">{{user.name}}</td>
        <td class="px-4 py-3">{{user.email}}</td>
        <td class="px-4 py-3">{{user.phone}}</td>
        <td class="px-4 py-3">{{user.address}}</td>
        <td class="px-4 py-3">{{user.country}}</td>
    </tr>
    </table>
  </div>
</template>

<script>
export default {
  name: 'CustomTable',
  props: ['msg']
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
