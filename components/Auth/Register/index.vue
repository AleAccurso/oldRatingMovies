<template>
  <div>
    <v-container class="grey lighten-5 mainLogo">
      <img src="../../../assets/logo_big.png" />
    </v-container>
    <v-container class="grey lighten-5 loginForm">
      <div class="loginTitle">
        <svg style="width:65px;height:65px" viewBox="0 0 24 24">
          <path
            fill="currentColor"
            d="M21.7 14.4L20.7 15.4L18.6 13.3L19.6 12.3C19.8 12.1 20.2 12.1 20.4 12.3L21.7 13.6C21.9 13.8 21.9 14.1 21.7 14.4M12 19.9L18.1 13.8L20.2 15.9L14.1 22H12V19.9M10 19.1L21 8.1V5L12 1L3 5V11C3 15.8 5.9 20.3 10 22.3V19.1Z"
          /></svg
        ><br />
        Register
      </div>
      <form @submit.prevent="register">
        <label for="password" class="form-label"></label>
        <div class="mb-3">
          <input
            type="text"
            placeholder="Name"
            v-model="registerData.name"
            class="form-control"
            id="name"
          />
        </div>
        <label for="password" class="form-label"></label>
        <div class="mb-3">
          <input
            type="email"
            placeholder="Email address"
            class="form-control"
            id="email"
            v-model="registerData.email"
            aria-describedby="emailHelp"
          />
        </div>
        <div class="mb-3">
          <label for="password" class="form-label"></label>
          <input
            type="password"
            placeholder="Password"
            v-model="registerData.password"
            class="form-control"
            id="password"
          />
        </div>
        <button type="submit" class="btn w-100 registerButton">Register</button>
      </form>
    </v-container>
  </div>
</template>

<script>
export default {
  data() {
    return {
      registerData: {
        name: "",
        email: "",
        password: ""
      }
    };
  },
  methods: {
    async register() {
      try {
        const user = await this.$axios.$post("/auth/signin", {
          name: this.registerData.name,
          email: this.registerData.email,
          password: this.registerData.password
        });
      } catch (err) {
        console.log(err);
      }
      this.$router.push("/auth/login");
    }
  }
};
</script>

<style>
.loginForm {
  width: 800px;
  padding: 50px;
  background-color: #ffffff20;
  border-radius: 14px;
  margin-top: 30px;
}
.loginTitle {
  color: #ffffff79;
  font-family: "Ubuntu", sans-serif;
  text-align: center;
  font-weight: 500;
  font-size: 50px;
}
.registerButton {
  color: #fff;
  background-color: #a52199;
  font-family: "Lato", sans-serif;
  margin-top: 10px;
  font-weight: 500;
  font-size: 17px;
}
#name {
  color: #a52199;
  font-family: "Lato", sans-serif;
  font-weight: 500;
  font-size: 17px;
}
#email {
  color: #a52199;
  font-family: "Lato", sans-serif;
  font-weight: 500;
  font-size: 17px;
}
#password {
  color: #a52199;
  font-family: "Lato", sans-serif;
  font-weight: 500;
  font-size: 17px;
}
</style>
