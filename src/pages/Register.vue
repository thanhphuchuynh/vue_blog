<template>
  <div class="login">
    <div>
      <form @submit.prevent="submit">
        <div>
          <label for="name">name:</label>
          <input type="text" name="name" v-model="form.name" />
        </div>
        <div>
          <label for="email">email:</label>
          <input type="text" name="email" v-model="form.email" />
        </div>
        <div>
          <label for="password">Password:</label>
          <input type="password" name="password" v-model="form.password" />
        </div>
        <button type="submit">Submit</button>
      </form>
      <p v-if="showError" id="error">Username or Password is incorrect</p>
    </div>
  </div>
</template>

<script>
import { mapActions } from "vuex";
export default {
  name: "Register",
  components: {},
  data() {
    return {
      form: {
        email: "",
        password: "",
        name: "",
      },
      showError: false
    };
  },
  methods: {
    ...mapActions(["Register"]),
    async submit() {
      console.log(this.form)
      try {
          await this.Register(this.form);
          this.$router.push("/login");
          this.showError = false
      } catch (error) {
        this.showError = true
      }
    },
  },
};
</script>

<style scoped>
* {
  box-sizing: border-box;
}
label {
  padding: 12px 12px 12px 0;
  display: inline-block;
}
button[type="submit"] {
  background-color: #4caf50;
  color: white;
  padding: 12px 20px;
  cursor: pointer;
  border-radius: 30px;
}
button[type="submit"]:hover {
  background-color: #45a049;
}
input {
  margin: 5px;
  box-shadow: 0 0 15px 4px rgba(0, 0, 0, 0.06);
  padding: 10px;
  border-radius: 30px;
}
#error {
  color: red;
}
</style>