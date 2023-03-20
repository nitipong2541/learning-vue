<template>
  <ui-popup :open="pop" @close="pop = !pop">{{ textpop }}</ui-popup>
  <div class="border-4 border-gray-600 justify-center w-60 rounded-lg">
    <div>
      <div class="bg-sky-700 p-2 text-white text-2xl">Sign-In</div>
      <div class="m-2" :class="{ shake: shakingUser }">
        <div class="flex">
          <label :class="[shakingUser ? 'text-red-600' : 'text-black']">Username</label>
        </div>
        <input
          ref="username"
          v-model="username"
          type="username"
          class="border-2 border-gray-700 rounded-lg px-2"
          :class="[shakingUser ? ['border-2', '!border-red-600'] : '']"
          autofocus
        />
      </div>
      <div class="m-2" :class="{ shake: shakingPass }">
        <div class="flex">
          <label :class="[shakingPass ? 'text-red-600' : 'text-black']">Password</label>
        </div>
        <input
          ref="password"
          v-model="password"
          type="password"
          class="border-2 border-gray-700 rounded-lg px-2"
          :class="[shakingPass ? ['border-2', '!border-red-600'] : '']"
        />
      </div>
    </div>
    <div class="justify-center flex m-2">
      <ui-button @click="signinBtn" ref="signin" icon1="login" text="sign-in"
        >Sign-in
        <template #icon2><img src="../assets/logo.png" class="w-5 h-5" /></template>
      </ui-button>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  data() {
    return {
      username: "",
      password: "",
      textpop: "",
      shakingUser: false,
      shakingPass: false,
    };
  },
  setup() {
    const pop = ref(false);

    return { pop };
  },
  computed: {
    disableSignIn() {
      return this.username == "" || this.password == "";
    },
  },
  mounted() {
    this.$refs.username.focus();
  },

  methods: {
    signinBtn() {
      if (this.username != "") {
        if (this.password != "") {
          if (this.username == "admin") {
            if (this.password == "1234") {
              this.$router.push("/pform");
            } else {
              this.textpop = "Invalid password";
              this.pop = true;
            }
          } else {
            this.textpop = "Invalid username";
          }
          this.pop = true;
        } else {
          this.shakingPass = true;
          setTimeout(() => {
            this.shakingPass = false;
          }, 1500);
        }
      } else {
        this.shakingUser = true;
        setTimeout(() => {
          this.shakingUser = false;
        }, 1500);
      }
    },
  },
};
</script>

<style>
.shake {
  animation: shake 0.82s cubic-bezier(0.36, 0.07, 0.19, 0.97) both;
  transform: translate3d(0, 0, 0);
}

@keyframes shake {
  10%,
  90% {
    transform: translate3d(-1px, 0, 0);
  }

  20%,
  80% {
    transform: translate3d(2px, 0, 0);
  }

  30%,
  50%,
  70% {
    transform: translate3d(-4px, 0, 0);
  }

  40%,
  60% {
    transform: translate3d(4px, 0, 0);
  }
}
</style>
