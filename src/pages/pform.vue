<template>
  <div class="border-2 w-220">
    <form v-on:submit.prevent="addNewName">
      <div class="ml-30 my-5">
        <div class="m-2 flex">
          <div class="pr-2"><label>Name</label></div>
          <input v-model="newName" type="text" class="border-2 border-gray-700" />
          <div class="pl-8 pr-2"><label>Lastname</label></div>
          <input v-model="newLastname" type="text" class="border-2 border-gray-700" />
        </div>
        <div class="m-2 flex">
          <div class="pr-5"><label>Age</label></div>
          <input v-model="newAge" type="number" class="border-2 border-gray-700" />
          <div class="pl-3 pr-2"><label>Date of birth</label></div>
          <input v-model="newDate" type="date" class="border-2 border-gray-700" />
        </div>
      </div>

      <div>
        <button class="mb-2 border-2 border-lime-700 bg-lime-300"><p>Add</p></button>
      </div>
    </form>
    <div>
      <button
        type="button"
        @click="createDataList"
        class="mb-2 border-2 border-black bg-gray-200"
      >
        [____]
      </button>
      <button @click="watchBtn">watch data</button>
    </div>
  </div>
  <!-- <div class="border-2 w-220 mt-5">
    <div>
      <ul>
        <p-List-Mdule
          v-on:saveBtn="updatData($event)"
          v-for="(nlist, index) in nameLists"
          :key="nlist.id"
          :name="nlist.name"
          :lastname="nlist.lastname"
          :age="nlist.age"
          :dob="nlist.dob"
          @remove="nameLists.splice(index, 1)"
        ></p-List-Mdule>
      </ul>
    </div>
  </div> -->
  <div>
    <ui-table :rows="datalist" :cols="columns">
      <template #edit="data">
        <ui-button
          v-if="data.row.editmode"
          class="!w-10 !h-8 !bg-lime-800"
          @click="saveBtn(data)"
          >Save</ui-button
        >
        <ui-button v-else class="!w-10 !h-8 bg-gray-700" @click="editBtn(data)"
          >Edit</ui-button
        ></template
      >
      <template #delete="data">
        <ui-button
          v-if="data.row.editmode"
          class="!w-15 !h-8 !bg-orange-500"
          @click="cancelBtn(data)"
          >Cancle</ui-button
        >
        <ui-button v-else class="!w-15 !h-8 !bg-red-600" @click="deleteBtn(data)"
          >Delete</ui-button
        ></template
      >
    </ui-table>

    <div>
      {{ saveOnEdits }}
    </div>
    <div>
      {{ datalist }}
    </div>
  </div>
</template>

<script>
import pListMdule from "../components/pListMdule.vue";
export default {
  component: { pListMdule },
  data() {
    const datalist = [];
    // datalist.push({
    //   id: 1,
    //   firstname: "Vill",
    //   lastname: "V",
    //   age: 12,
    //   dob: "2222-2-2",
    // });
    // datalist.push({
    //   id: 2,
    //   firstname: "elly",
    //   lastname: "p",
    //   age: 23,
    //   dob: "2211-12-12",
    // });
    console.log(datalist);
    return {
      newName: "",
      newLastname: "",
      newAge: "",
      newDate: "",
      nameLists: [],
      columns: [
        { id: "firstname", text: "Name" },
        { id: "lastname", text: "Lastname" },
        { id: "age", text: "Age" },
        { id: "date", text: "Birth day " },
        { id: "edit", text: "" },
        { id: "delete", text: "" },
      ],
      nextNameId: 1,
      datalist,
      editting: false,
      saveOnEdits: [],
    };
  },
  methods: {
    addNewName() {
      console.log(this.datalist);
      // this.nameLists.push({
      //   id: this.nextNameId++,
      //   name: this.newName,
      //   lastname: this.newLastname,
      //   age: this.newAge,
      //   dob: this.newDate,
      // });
      this.datalist.push({
        id: this.nextNameId++,
        firstname: this.newName,
        lastname: this.newLastname,
        age: this.newAge,
        date: this.newDate,
        editmode: false,
      });

      this.newName = "";
      this.newLastname = "";
      this.newAge = "";
      this.newDate = "";
    },
    updatData() {},
    createDataList() {
      for (let i = 0; i < 10; i++) {
        const d = new Date();
        let month = (d.getMonth() + 1).toString();
        if (d.getMonth() < 9) {
          month = "0" + month;
        }
        this.datalist.push({
          id: this.nextNameId,
          firstname: "Firstname" + this.nextNameId,
          lastname: "Lastname" + this.nextNameId,
          age: 20 + this.nextNameId,
          date: d.getFullYear() + "-" + month + "-" + d.getDate(),
          editmode: false,
        });
        this.nextNameId++;
      }
    },
    editBtn(data) {
      // data.row.firstname = "Jesus";
      this.saveOnEdits.push({
        i: data.row.id,
        fn: data.row.firstname,
        ln: data.row.lastname,
        a: data.row.age,
        d: data.row.date,
      });
      data.row.editmode = true;
      this.editting = true;
    },
    deleteBtn(data) {
      this.datalist.splice(data.idx, 1);
      console.log(data.row.id + " deleted");
    },
    saveBtn(data) {
      for (let i = 0; i < this.saveOnEdits.length; i++) {
        if (this.saveOnEdits[i].i == data.row.id) {
          this.saveOnEdits.splice(i, 1);
          return;
        }
      }
      this.editting = false;
      data.row.editmode = false;
      console.log("save");
    },
    cancelBtn(data) {
      this.editting = false;
      data.row.editmode = false;
      for (let i = 0; i < this.saveOnEdits.length; i++) {
        if (this.saveOnEdits[i].i == data.row.id) {
          data.row.id = this.saveOnEdits[i].i;
          data.row.firstname = this.saveOnEdits[i].fn;
          data.row.lastname = this.saveOnEdits[i].ln;
          data.row.age = this.saveOnEdits[i].a;
          data.row.date = this.saveOnEdits[i].d;
          this.saveOnEdits.splice(i, 1);
          return;
        }
      }
    },
    watchBtn() {
      console.log(this.datalist);
      console.log(this.saveOnEdits);
      const d = new Date();
      console.log(d.getMonth());
    },
  },
};
</script>
