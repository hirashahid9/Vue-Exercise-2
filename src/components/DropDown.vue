<template>
  <div class="w-40 m-auto shadow-xl">
    <button @click.prevent="visible=!visible" class="w-full text-left bg-white rounded-t hover:bg hover:bg-gray-200">{{selected}}</button>
    <div v-if="visible" class="w-full px-1 pt-1 m-auto bg-white rounded-lg ">
      <div v-for="item in options" :key="item.id">
      <a href="#" @click="changeSelected(item)" class="block text-left border-b-2 bg-gray-150 hover:bg-gray-200">{{item.title}}</a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'DropDown',
  props: {
    options: Array
  },
  data()
  {
    return {
      visible: false,
      selected: 'Select an option'
    }
  },
  methods: {
        changeSelected: function(value){
          this.selected=value.title
          this.visible=false
          this.$emit('show-option',value)
        }
    },
}
</script>

