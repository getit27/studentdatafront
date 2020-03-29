<template>
  <div id="search">
    <h2>SEARCH:</h2>
    <h2>{{ name }}</h2>
    <table>
      <thead>
        <tr>
          <th>name</th>
          <th>sex</th>
          <th>birth date</th>
          <th>native place</th>
          <th>department</th>
          <th>student number</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="student in result" :key="student.id">
          <td v-if="editid==student.id">
            <input type="text" v-model="edited.name" />
          </td>
          <td v-else>{{ student.name }}</td>

          <td v-if="editid==student.id">
            <input type="text" v-model="edited.sex" />
          </td>
          <td v-else>{{ student.sex }}</td>

          <td v-if="editid==student.id">
            <input type="text" v-model="edited.bd" />
          </td>
          <td v-else>{{student.bd}}</td>

          <td v-if="editid==student.id">
            <input type="text" v-model="edited.np" />
          </td>
          <td v-else>{{student.np}}</td>

          <td v-if="editid==student.id">
            <input type="text" v-model="edited.department" />
          </td>
          <td v-else>{{student.department}}</td>

          <td v-if="editid==student.id">
            <input type="text" v-model="edited.sn" />
          </td>
          <td v-else>{{student.sn}}</td>

          <td v-if="editid==student.id">
            <button v-on:click.prevent="save">Save</button>
            <button v-on:click.prevent="cancel">Cancel</button>
          </td>
          <td v-else>
            <button v-on:click.prevent="edit(student.id)">Edit</button>
            <button v-on:click.prevent="delet(student.id)">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "search",
  props: {
    result: Array,
    name: String
  },
  methods: {
    delet(id) {
      this.$emit("delete:student", id);
    },
    edit(id) {
      for (var i = 0; i < this.result.length; i++) {
        if (this.result[i].id == id) {
          this.edited.id = this.result[i].id;
          this.edited.name= this.result[i].name;
          this.edited.sex= this.result[i].sex;
          this.edited.bd= this.result[i].bd;
          this.edited.np= this.result[i].np;
          this.edited.department= this.result[i].department;
          this.edited.sn= this.result[i].sn;
          break;
        }
      }
      this.editid = id;
    },
    cancel() {
      this.editid = -1;
    },
    save() {
      if (
        this.edited.name != "" &&
        this.edited.sex != "" &&
        this.edited.bd != "" &&
        this.edited.np != "" &&
        this.edited.department != "" &&
        this.edited.sn != ""
      ) {
        this.$emit("edit:student", this.edited);
        this.editid=-1;
      }
    }
  },
  data() {
    return {
      editid: -1,
      edited: {
        id: -1,
        name: "",
        sex: "",
        bd: "",
        np: "",
        department: "",
        sn: ""
      }
    };
  }
};
</script>

<style scoped>
</style>