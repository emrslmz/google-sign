<template>
  <div id="app">
    <div>
      <h2>Google Sign</h2>
      <img class="login-button" width="200px" src="../src/assets/google-login.png" alt="google-login-button" @click="login()" v-show="!isLogin" />
      <div>
        Login mi ? {{ isLogin }}
        <br>
        <p class="logout-button" @click="logOut()" v-show="isLogin">Çıkış Yap</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      isLogin: false,
    };
  },
  methods: {
    async logOut() {
      const result = await this.$gAuth.signOut();
      this.isLogin = false;
      console.log(`result`, result);
    },
    async login() {
      const googleUser = await this.$gAuth.signIn();
      console.log("googleUser", googleUser);
      console.log("getId", googleUser.getId());
      console.log("getBaseProfile", googleUser.getBasicProfile());
      console.log("getAuthResponse", googleUser.getAuthResponse());
      console.log(
          "getAuthResponse$G",
          this.$gAuth.GoogleAuth.currentUser.get().getAuthResponse()
      );
      this.isLogin = this.$gAuth.isAuthorized;
    },
  },
};
</script>

<style>
#app {
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.login-button {
  cursor: pointer;
}

.logout-button {
  cursor: pointer;
  color: blue;
  text-decoration: underline;
}
</style>
