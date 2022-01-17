<template>
  <form @submit.prevent="handleSubmit">

    <label>Email:</label>
    <input type="email" required v-model="email">

    <div style="position: relative">
      <label>Password:</label>
      <input :type="inputType" required v-model="password">
      <i @click="togglePassword" class="far fa-eye-slash"></i>
      <div v-if="passwordError" class="error">{{passwordError}}</div>
    </div>

    <label>Role:</label>
    <select v-model="role">
      <option value="select">Select Role</option>
      <option value="developer">Web Developer</option>
      <option value="designer">Web Designer</option>
      <option value="believer">Believer</option>
    </select>

    <label>Skills:</label>
    <input type="text" v-model="tempSkill" @keyup="addSkill" @keydown.enter.prevent>

    <ul class="skills">
      <li class="skill" v-for="skill in skills" :key="skill" @click="deleteSkill(skill)" @mouseover="deleteSkillOver">
        {{skill}}
      </li>
    </ul>

    <div class="terms">
      <input type="checkbox" required v-model="terms">
      <label>Accept terms and condition</label>
    </div>

    <div class="submit">
      <button>Create an account</button>
    </div>

    <!-- <div>
      <input type="checkbox" value="elena" v-model="names">
      <label>Elena</label>
    </div>
    <div>
      <input type="checkbox" value="mario" v-model="names">
      <label>Mario</label>
    </div>
    <div>
      <input type="checkbox" value="luigi" v-model="names">
      <label>Luigi</label>
    </div> -->
  </form>
</template>

<script>
export default {
  data() {
    return {
      email: '',
      password: '',
      showPassword: false,
      inputType: 'password',
      role: 'select',
      terms: false,
      // names: []
      tempSkill: '',
      skills: [],
      passwordError: ''
    }
  },
  methods: {
    togglePassword() {
      this.showPassword = !this.showPassword
      if(this.showPassword){
        this.inputType = 'text'
      }else{
        this.inputType = 'password'
      }
    },
    addSkill(e) {
      if (e.key === 'Enter' && this.tempSkill) {
        if (!this.skills.includes(this.tempSkill)) {
          this.skills.push(this.tempSkill)
        }
        this.tempSkill = ''
      }
    },
    deleteSkill(skill) {
      this.skills = this.skills.filter((item) => {
        return skill !== item
      })
    },
    deleteSkillOver() {

    },
    handleSubmit() {
      // Password validation
      this.passwordError = this.password.length >= 8 ?
      '': 'The passoword must be at least 8 characters long' 
    }
  }
}
</script>

<style>
  form {
    max-width: 420px;
    margin: 30px auto;
    background: white;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
  }
  label {
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 0.6em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
  }
  input, select {
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
  }
  input[type="checkbox"] {
    display: inline-block;
    width: 16px;
    margin: 0 10px 0 0;
    position: relative;
    top: 2px;
  }
  ul {
    padding-inline-start: 0;
  }
  .skill {
    display: inline-block;
    margin: 20px 10px 0 0;
    padding: 6px 12px;
    background: #eee;
    border-radius: 20px;
    font-size: 12px;
    letter-spacing: 1px;
    font-weight: bold;
    color: #777;
    cursor: pointer;
  }
   button {
    background: #0b6dff;
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 20px;
    cursor: pointer;
  }
  .submit {
    text-align: center;
  }
  .error {
    color: #ff0062;
    margin-top: 10px;
    font-size: 0.8em;
    font-weight: bold;
  }
  .fa-eye-slash {
    position: absolute;
    top: 64px;
    right: 5px;
    cursor: pointer;
  }
</style>