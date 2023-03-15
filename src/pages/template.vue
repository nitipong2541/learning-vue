<template>
  <div class="text-bold" :title="'Age ' + age">
    Name : {{ name.toUpperCase() }} {{ lastname }}
  </div>

  <div>line 2</div>
  <div class="py-2">
    <button type="button" @click="ButtonClick" class="border-1 border-black mr-2">
      x++
    </button>
    <button type="button" @click="ButtonClick2" class="border-1 border-black mr-2">
      y++
    </button>
    <button type="button" @click="ResetBCount" class="border-1 border-black">
      Reset
    </button>
  </div>
  <div v-for="n1 in bCount" :key="n1" class="flex">
    <div v-for="n2 in bCount2" :key="n2" class="mr-1">[{{ n1 }} ,{{ n2 }}]</div>
  </div>
  <div>
    <form v-on:submit.prevent="addNewList">
      <label for="new-textList">Add new text</label>
      <input
        v-model="newListTitle"
        id="new-textList"
        placeholder="some text"
        class="ml-2 border-2 border-gray-500"
      />
      <button>Add</button>
    </form>
    <ul>
      <list-module
        v-for="(textList, index) in listMs"
        :key="textList.id"
        :title="textList.title"
        @remove="listMs.splice(index, 1)"
      ></list-module>
    </ul>
  </div>

  <button @click="PushSignin">go to /signin</button>
</template>

<script>
import ListModule from "../components/ListModule.vue";

export default {
  component: { ListModule },
  data() {
    return {
      name: "Eman",
      lastname: "Emantsal",
      vbind: "Attribute Bindings",
      age: 28,
      buttonDisable: false,
      bCount: 1,
      bCount2: 1,
      newListTitle: "",
      listMs: [],
      nextListId: 0,
    };
  },
  methods: {
    PushSignin() {
      this.$router.push("/signin");
    },
    ButtonClick() {
      this.bCount++;
    },
    ButtonClick2() {
      this.bCount2++;
    },
    ResetBCount() {
      this.bCount = 1;
      this.bCount2 = 1;
    },
    addNewList() {
      this.listMs.push({
        id: this.nextListId++,
        title: this.newListTitle,
      });
      this.newListTitle = "";
    },
  },
};
</script>

<style>
.text-bold {
  font-weight: bold;
  font-size: 30px;
  font-style: italic;
}
</style>
