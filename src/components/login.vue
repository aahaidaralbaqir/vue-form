<template>
  <form class="form" @submit.prevent="submit">
    <h1>Login page</h1>
    <ui-input 
      name="username"
      :value="username.value"
      type="text"
      :rules="{required: true, min: 5}"
      @update="update"
    />
    <ui-input 
      name="password"
      :value="password.value"
      type="password"
      :rules="{required: true, min: 5}"
      @update="update"
    />
    <ui-button 
      color="white"
      background="darkslateblue"
      :disabled="!valid"
    />
    
  </form>
</template>

<script>
import button from "./button";
import input from "./input";
export default {
  components: {
    "ui-button": button,
    "ui-input": input
  },
  data: () => ({
    username: {
      value: "",
      valid: false
    },
    password: {
      value: "",
      valid: false
    }
  }),
  computed: {
    valid() {
      return this.username.valid && this.password.valid
    }
  },
  methods: {
    submit() {
      console.log("reqlaksjdalksjd")
    },
    update(payload) {
      this[payload.name.toLowerCase()]= {
        value: payload.value,
        valid: payload.valid
      }
    }
  }
}
</script>

<style scoped>
  .form {
    max-width: 400px;
    width: 50%;
  }
</style>