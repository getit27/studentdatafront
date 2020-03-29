<template>
  <div id="add-form">
    <h2>ADD</h2>
    <form>
      <label>Name</label>
      <br />
      <input type="text" v-model="newData.name" />
      <label v-if="this.error.name&&this.invalidName">empty</label>
      <br />
      <label>Sex</label>
      <br />
      <input type="text" v-model="newData.sex" />
      <label v-if="this.error.sex&&this.invalidSex">empty</label>
      <br />
      <label>Birth Date</label>
      <br />
      <input type="text" v-model="newData.bd" />
      <label v-if="this.error.bd&&this.invalidBd">empty</label>
      <br />
      <label>Native Place</label>
      <br />
      <input type="text" v-model="newData.np" />
      <label v-if="this.error.np&&this.invalidNp">empty</label>
      <br />
      <label>Department</label>
      <br />
      <input type="text" v-model="newData.department" />
      <label v-if="this.error.department&&this.invalidDepartment">empty</label>
      <br />
      <label>Student Number</label>
      <br />
      <input type="text" v-model="newData.sn" />
      <label v-if="this.error.sn&&this.invalidSn">empty</label>
      <br />
      <button v-on:click.prevent="submit">Add Student</button>
      <br />
      <button v-on:click.prevent="switchRoot">Cancel</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "addform",
  methods: {
    switchRoot() {
      this.$emit("switch:status", 1);
    },
    submit() {
      this.submiting = true;
      if (
        !this.invalidName &&
        !this.invalidSex &&
        !this.invalidBd &&
        !this.invalidBd &&
        !this.invalidNp &&
        !this.invalidDepartment &&
        !this.invalidSn
      ) {
        this.$emit("switch:status", 1);
        this.$emit("add:student", this.newData);
      }
      {
        this.error.name = this.invalidName;
        this.error.sex = this.invalidSex;
        this.error.bd = this.invalidBd;
        this.error.np = this.invalidNp;
        this.error.department = this.invalidDepartment;
        this.error.sn= this.invalidSn;
      }
    }
  },
  data() {
    return {
      submiting: false,
      success: false,
      newData: {
        name: "",
        sex: "",
        bd: "",
        np: "",
        department: "",
        sn: ""
      },
      error: {
        name: false,
        sex: false,
        bd: false,
        np: false,
        department: false,
        sn: false
      }
    };
  },
  computed: {
    invalidName() {
      return this.newData.name == "";
    },
    invalidSex() {
      return this.newData.sex == "";
    },
    invalidBd() {
      return this.newData.bd == "";
    },
    invalidNp() {
      return this.newData.np == "";
    },
    invalidDepartment() {
      return this.newData.department == "";
    },
    invalidSn() {
      return this.newData.sn == "";
    }
  }
};
</script>

<style scoped>
</style>