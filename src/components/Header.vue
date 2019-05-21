<template>
  <header class="background-primary color-white padding-md height-md flex between middle margin-bottom-md">
    <div class="flex middle">
    <h1 class="font-weight-7 margin-right-lg">React My App</h1>
    <input @keyup="inputChange" :value="value" @input="updateValue($event.target.value)" class="radius-max height-sm padding-md header-search" placeholder="arama" type="text"/>
    </div>
      <nav>
        <ul class="flex">
          <li class="margin-right-md">
            <router-link to="/">Home</router-link>
          </li>
          <li>
            <router-link to="/about/">About</router-link>
          </li>
      </ul>
    </nav>
  </header>
</template>

<script>
export default {
  name: 'Header',
  props: ['value'],
  methods: {
    updateValue: function (value) {
      this.$emit('input', value);
    },
    inputChange(){
      this.$parent.inputChange();
    }
  },
  data(){
    return{
      
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .header-search{
    width: 30rem;
  }
</style>
