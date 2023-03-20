<template>
  <li>
    <div v-if="edit" class="flex m-1 border-2 pl-4">
      <button @click="cancleBtn" class="border-2 border-red-600 w-30 h-10 m-1">
        Cancle
      </button>
      <button @click="saveBtn" class="border-2 border-orange-400 w-20 h-10 m-1">
        Save
      </button>
      <div class="flex h10">
        <div class="w-40 flex">
          <input class="w-40" type="text" v-model="eName" :placeholder="name" />
        </div>
        <div class="w-40 flex">
          <input class="w-40" type="text" v-model="eLastname" :placeholder="lastname" />
        </div>
        <div class="w-10">
          <input class="w-40" type="number" v-model="eAge" :placeholder="age" />
        </div>
        <div class="w-50">
          <input class="w-40" type="date" v-model="eDate" :placeholder="dob" />
        </div>
      </div>
    </div>

    <div v-else class="flex m-1 border-2 pl-4">
      <button @click="$emit('remove')" class="border-2 border-red-600 w-30 h-10 m-1">
        Remove
      </button>
      <button @click="editBtn" class="border-2 border-orange-400 w-20 h-10 m-1">
        Edit
      </button>
      <div class="flex h10">
        <div class="w-40 flex">
          <label for="text">{{ name }}</label>
        </div>
        <div class="w-40 flex">
          <label for="text">{{ lastname }}</label>
        </div>
        <div class="w-10">
          <label for="number">{{ age }}</label>
        </div>
        <div class="w-50">
          <label for="date">{{ dob }}</label>
        </div>
      </div>
    </div>
  </li>
</template>

<script>
export default {
  props: ["name", "lastname", "age", "dob"],
  emits: ["remove"],
  data() {
    return {
      c: 0,
      edit: false,
      eName: "",
      eLastname: "",
      eAge: "",
      eDate: "",
    };
  },
  methods: {
    editBtn() {
      this.eName = this.name;
      this.eLastname = this.lastname;
      this.eAge = this.age;
      this.eDate = this.dob;
      this.edit = true;
    },
    cancleBtn() {
      this.eName = "";
      this.eLastname = "";
      this.eAge = "";
      this.eDate = "";
      this.edit = false;
    },
    saveBtn: function () {
      this.$emit("saveBtn", [this.eName, this.eLastname, this.eAge, this.eDate]);
      this.edit = false;
    },
  },
};
</script>
