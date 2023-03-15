<template>
  <div class="text-bold" :title="'Age ' + age">
    Name : {{ name.toUpperCase() }} {{ lastname }}
  </div>
  <div>line 2</div>
  <button :disabled="buttonDisable">Button</button>
  <button @click="PushSignin">go to /signin</button>
</template>

<script>
export default {
  data() {
    return {
      name: "Eman",
      lastname: "Emantsal",
      vbind: "Attribute Bindings",
      age: 28,
      buttonDisable: false,
    };
  },
  methods: {
    PushSignin() {
      this.$router.push("/signin");
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
