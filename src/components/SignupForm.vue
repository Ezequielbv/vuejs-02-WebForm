<template>
  <form @submit.prevent="handleSubmit">
    <label>Email:</label>
    <input type="email" required v-model="email" />
    <label>Password:</label>
    <input type="password" required v-model="password" />
    <div v-if="passwordError" class="error">{{ passwordError }}</div>

    <label> Role:</label>
    <select v-model="role">
      <option value="developer">Web Developer</option>
      <option value="designer">Web Designer</option>
    </select>

    <label>Skills:</label>
    <input type="text" v-model="tempSkill" @keyup.ctrl="addSkill" />
    <div v-for="skill in skills" :key="skill" class="pill">
      <span @click="removeSkill(skill)">{{ skill }}</span>
    </div>

    <div class="terms">
      <input type="checkbox" v-model="terms" required />
      <label> Accept terms and conditions</label>
    </div>

    <div class="submit">
      <button>Create an Account</button>
    </div>

    <!-- <div>
        <input type="checkbox" value="shaun" v-model="name">
        <label for="">Shaun</label>
    </div>
    <div>
        <input type="checkbox" value="yoshi" v-model="name">
        <label for="">Yoshi</label>
    </div>
    <div>
        <input type="checkbox" value="mario" v-model="name">
        <label for="">Mario</label>
    </div> -->
  </form>

  <!-- <p>Email: {{ email }}</p>
  <p>Password: {{ password }}</p>
  <p>Role: {{ role }}</p>
  <p>Skills: {{ skills }}</p>
  <p>Terms accepted: {{ terms }}</p> -->
  <!-- <p>Names: {{ name }}</p> -->
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "",
      terms: false,
      tempSkill: "",
      skills: [],
      passwordError: "",
      //   name: [],
    };
  },
  methods: {
    addSkill(e) {
      if (e.key === "," && this.tempSkill) {
        if (!this.skills.includes(this.tempSkill)) {
          this.skills.push(this.tempSkill);
        }
        console.log(e);
        this.tempSkill = "";
      }
    },
    removeSkill(skill) {
      this.skills = this.skills.filter((item) => {
        return skill !== item;
      });
    },
    handleSubmit() {
      // validate password
      this.passwordError =
        this.password.length > 5
          ? ""
          : "Password must be at least 6 chars long";
        
        if (!this.passwordError) {
            console.log('email: ', this.email)
            console.log('password: ', this.password)
            console.log('role: ', this.role)
            console.log('skills: ', this.skills)
            console.log('terms accepted: ', this.terms)
        }
    },
  },
};
</script>

<style>
form {
  max-width: 420px;
  margin: 30px auto;
  padding: 40px;
  background: white;
  text-align: left;
  border-radius: 10px;
}
label {
  display: inline-block;
  margin: 25px 0 15px;
  font-size: 0.6em;
  color: #aaa;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}
input,
select {
  display: block;
  width: 100%;
  padding: 10px 6px;
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
.pill {
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
  margin-top: 20px;
  padding: 10px 20px;
  background: #0b6dff;
  color: #fff;
  border: 0;
  border-radius: 20px;
}
.submit {
  text-align: center;
}
.error {
  margin-top: 10px;
  color: #ff0062;
  font-size: 0.8em;
  font-weight: bold;
}
</style>