<template>
  <div id="root-form">
    <form>
      <label>Name</label>
      <br />
      <input type="text" v-model="name"/>
      <!--to be done-->
      <br />
      <button v-on:click.prevent="switchSearch">Search Student</button>
      <br />
      <button v-on:click.prevent="switchAdd">Add Student</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "rootform",
  methods: {
    switchAdd() {
      this.$emit("switch:status", 0);
    },
    switchSearch(){
      this.$emit("search:students",this.name);
      this.$emit("switch:status",2);
    }
  },
  data(){
    return{
      name:""
    }
  }
};
</script>

<style scoped>
</style>