<template>
  <form @submit.prevent="submit">
    <label for="email">Email:</label>
    <input type="email" id="email" required v-model="email" />

    <label for="password">Password:</label>
    <input type="password" id="password" v-model="password" />
    <div v-if="passwordError" class="error">{{ passwordError }}</div>
    <label for="age">Age:</label>
    <input type="number" id="age" v-model="age" />
    <label for="skill">Skills: </label>
    <input id="skill" type="text" @keyup="addSkill" v-model="tempSkill" />
    <div :key="skill" v-for="skill in skills" class="pill">
      <span @click="deleteSkill(skill)">{{ skill }}</span>
    </div>

    <div class="terms">
      <input id="termAndCondition" type="checkbox" required v-model="terms" />
      <label for="termAndCondition" class="terms"
        >Accept terms and condition</label
      >
    </div>
    <div class="submit">
      <button type="submit">Create an Account</button>
    </div>
  </form>
</template>

<script>
export default {
  name: "SingleForm",
  data() {
    return {
      email: "",
      password: "",
      age: null,
      terms: false,
      tempSkill: "",
      skills: [],
      passwordError: false,
    };
  },
  methods: {
    addSkill(e) {
      if (e.key === "," && this.tempSkill) {
        if (!this.skills.includes(this.tempSkill))
          this.skills.push(this.tempSkill);
        this.tempSkill = "";
      }
    },
    deleteSkill(skill) {
      this.skills = this.skills.filter((item) => {
        return item !== skill;
      });
    },
    submit() {
      console.log("form Submitted");
      // validate the password
      this.passwordError =
        this.password.length > 5 ? "" : "Password must be atLeast 6 chars long";
      if (!this.passwordError) {
        console.log(this.email);
        console.log(this.password);
        console.log(this.age);
        console.log(this.skills);
      }
    },
  },
};
</script>

<style scoped>
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

input {
  display: block;
  padding: 10px 6px;
  width: 100%;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
}

input[type="checkbox"] {
  display: inline-block;
  width: 21px;
  height: 13px;
  margin: 0 16px 0 0;
  position: relative;
  top: 2px;
}

.terms {
  text-transform: uppercase;
}

.pill {
  display: inline-block;
  margin: 20px 10px 0 0;
  padding: 6px 12px;
  border-radius: 20px;
  font-size: 12px;
  letter-spacing: 1px;
  font-weight: bold;
  color: #777;
  background: #eeeeee;
}

button {
  background: #0b6dff;
  border: 0;
  padding: 10px 20px;
  margin-top: 20px;
  color: white;
  border-radius: 20px;
}

.submit {
  text-align: center;
}
.error {
  color: #ff0062;
  margin-top: 10px;
  font-size: 0.8rem;
  font-weight: bold;
}
</style>
