<template>
  <div class="p-4 border-blue-800 rounded-3xl drop-shadow-2xl border-2">
    <form>
      <div class="p-2 text-2xl">Sign-In</div>
      <div>
        <label for="username" class="text-blue-800 px-1 text-lg"
          >Username {{ username }}</label
        >
        <input
          type="text"
          id="username"
          v-model.trim.lazy="username"
          placeholder="Username"
          :disabled="busySignIn"
          class="px-2 py-1 border-2 border-gray-400 rounded-lg outline-black"
          :class="{ 'bg-gray-400': busySignIn, 'text-gray-800': busySignIn }"
        />
      </div>
      <div class="py-2">
        <label for="password" class="text-blue-800 px-2 text-lg">Password</label>
        <input
          type="password"
          id="password"
          v-model="password"
          placeholder="Password"
          :disabled="busySignIn"
          class="px-2 py-1 border-2 border-gray-400 rounded-lg outline-black"
          :class="{ 'bg-gray-400': busySignIn, 'text-gray-800': busySignIn }"
        />
      </div>
      <div class="flex">
        <input type="checkbox" id="remember" v-model="remember" class="p-1" />
        <label for="remember" class="p-2">Remember user</label>
      </div>
      <div>
        <button
          type="button"
          :disabled="disableSignIn || busySignIn"
          @click="SignInButton"
          class="px-2 border-2 border-black rounded-2xl mr-4"
          :class="[
            /*busySignIn ? 'bg-gray-400' : 'bg-gray-200',*/
            disableSignIn ? 'bg-gray-500' : 'bg-gray-100',
          ]"
        >
          Sign-in
        </button>
        <button
          type="reset"
          @click="Reset"
          class="px-3 border-2 border-black rounded-2xl bg-gray-100"
        >
          Reset
        </button>
      </div>
      <div class="drop-shadow-2xl">
        <button @click="PushTemplate">Go to /template</button>
      </div>
    </form>
  </div>
  <div
    v-if="busySignIn"
    class="fixed top-0 bottom-0 left-0 right-0 opacity-80 bg-gray-800"
  >
    <div class="text-white text-4xl pt-30">Please wait...</div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      username: "",
      password: "",
      remember: false,
      busySignIn: false,
    };
  },

  computed: {
    disableSignIn() {
      return this.username === "" || this.password === "";
    },
  },
  // created() {},
  methods: {
    SignInButton() {
      this.busySignIn = true;
      setTimeout(() => {
        this.busySignIn = false;
      }, 1500);
    },
    Reset() {
      this.username = "";
      this.password = "";
    },
    PushTemplate() {
      this.$router.push("/template");
    },
  },
};
</script>
