<template>
  <div class="input-wrapper">
    <div class="label">
      <label :for="name">{{ name }}</label>
      <span class="error">{{ error }}</span>
    </div>
    <input 
      :type="type"
      :id="name"
      :value="value"
      @input="input"
    />
  </div>
</template>

<script>
export default {
  props: {
    name: {
      type: String,
      required: true
    },
    rules: {
      type: Object
    },
    value: {
      type: String
    },
    type: {
      type: String
    }
  },
   computed: {
    error() {
      return this.validate(this.value)
    }
  },
  methods: {
    validate(value) {
      if(this.rules.required && value.length === 0) {
        return "required";
      }
      if(this.rules.min && value.length < this.rules.min) {
        return  `Minimum length is ${this.rules.min}`
      }
      return  "";
    },
    input($evt) {
      this.$emit('update',{
        name: this.name,
        value: $evt.target.value,
        valid: this.validate($evt.target.value) ? false : true
      })
    }
  }
}
</script>
  
<style scoped>
  .input-wrapper {
    display: flex;
    flex-direction: column;
  }
  .error {
    color: red;
  }
  .label {
    display: flex;
    justify-content: space-between;
  }
  input {
     background: none;
    color: black;
    border: 1px solid silver;
    border-radius: 5px;
    padding: 10px;
    font-size: 16px;
    cursor: pointer;
    margin: 5px 0;
  }
</style>