<template>
  <div>
    <h1>Student Data</h1>
    <div id="app">
      <div v-if="status==0">
        <Add v-on:switch:status="switchStatus" v-on:add:student="handleNew" />
      </div>
      <div v-if="status==1">
        <Root v-on:switch:status="switchStatus" v-on:search:students="search" />
      </div>
      <div v-if="status==2">
        <Search
          v-bind:result="result"
          v-bind:name="name"
          v-on:delete:student="deleteStudent"
          v-on:edit:student="editStudent"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Add from "./components/Add.vue";
import Root from "./components/Root.vue";
import Search from "./components/Search.vue";

export default {
  name: "App",
  components: {
    Add,
    Root,
    Search
  },
  data() {
    return {
      name: "default",
      status: 1,
      data: {
        name: "",
        sex: "",
        bd: "",
        np: "",
        department: "",
        sn: ""
      },
      students: [],
      result: []
    };
  },
  methods: {
    switchStatus(status) {
      this.status = status;
    },
    handleNew(newData) {
      this.data = newData;
      try {
        fetch("http://localhost:8083/students", {
          method: "POST",
          headers: {
            "Content-Type": "application/json"
          },
          body: JSON.stringify(this.data)
        });
      } catch (error) {
        console.error(error);
      }
      this.getStudents();
    },
    search(name) {
      this.name = name;
      this.getStudents();
    },
    async deleteStudent(id) {
      this.id = id;
      try {
        await fetch("http://localhost:8083/students/" + this.id, {
          method: "DELETE"
        });
      } catch (error) {
        console.error(error);
      }
      this.search(this.name);
    },
    async editStudent(student) {
      this.student = student;
      try {
        await fetch("http://localhost:8083/students/" + this.student.id, {
          method: "PUT",
          headers: {
            "Content-Type": "application/json"
          },
          body: JSON.stringify(this.student)
        });
      } catch (error) {
        console.error(error);
      }
      this.search(this.name);
    },
    async getStudents() {
      try {
        const response = await fetch("http://localhost:8083/students");
        const data = await response.json();
        if('_embedded' in data)
          this.students = data._embedded.students;
        if (this.name != "")
          this.result = this.students.filter((item, index, arr) => {
            this.fakeindex = index;
            this.fakearr = arr;
            return item.name == this.name;
          });
        else {
          this.result = this.students;
        }
      } catch (error) {
        console.error(error);
      }
    }
  }
};
</script>

<style>
</style>
