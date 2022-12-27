<template>
  <form @submit.prevent="formSubmit">
    <label class="formLabel">EMAIL:</label>
    <input type="email" required v-model="email" />

    <label class="formLabel">PASSWORD:</label>
    <input type="password" required v-model="password" />
    <div v-if="passwordValidation" class="error">{{ passwordValidation }}</div>

    <label class="formLabel">ROLE:</label>
    <select required v-model="role">
      <option value="">SELECT A ROLE</option>
      <option value="web Developer">WEB DEVELOPER</option>
      <option value="web Designer">WEB DESIGNER</option>
    </select>
    <label class="formLabel">SKILLS:</label>
    <input type="text" v-model="skillTemp" @keyup="addSkill" />
    <div class="skills" v-for="skill in skills" :key="skill">
      <div @click="deleteSkill(skill)">{{ skill }}</div>
    </div>
    <div class="formCheck">
      <input type="checkbox" required v-model="term" />
      <label>accept terms and conditions</label>
    </div>
    <button>Create an account</button>
  </form>
</template>

<script>
export default {
  name: "signup_form",
  data() {
    return {
      email: "",
      password: "",
      role: "",
      term: false,
      skillTemp: "",
      skills: [],
      passwordValidation: "",
      lowerCase: "",
      upperCase: "",
      number: "",
      specialChar: "",
    };
  },
  methods: {
    addSkill(e) {
      if (e.key === "," && this.skillTemp) {
        if (!this.skills.includes(this.skillTemp)) {
          this.skillTemp = this.skillTemp.slice(0, this.skillTemp.length - 1);
          this.skills.push(this.skillTemp);
        }
        this.skillTemp = "";
      }
    },
    deleteSkill(skill) {
      this.skills = this.skills.filter((item) => {
        return skill !== item;
      });
    },
    formSubmit() {
      this.lowerCase = new RegExp("(?=.*[a-z])");
      this.upperCase = new RegExp("(?=.*[A-Z])");
      this.number = new RegExp("(?=.*[0-9])");
      this.specialChar = new RegExp('(?=.*[!@#$%^&*(),.?":{}|<>])');
      if (this.password.length < 8) {
        this.passwordValidation =
          "Password length should be more than 8 characters";
      } else if (!this.lowerCase.test(this.password)) {
        this.passwordValidation =
          "Password must contain a lower case character";
      } else if (!this.upperCase.test(this.password)) {
        this.passwordValidation =
          "Password must contain an upper case character";
      } else if (!this.number.test(this.password)) {
        this.passwordValidation = "Password must contain a numerical value";
      } else if (!this.specialChar.test(this.password)) {
        this.passwordValidation = "Password must contain a special Character";
      } else {
        this.passwordValidation = "";
      }
    },
  },
};
</script>

<style scoped>
form {
  width: 90%;
  margin-left: 6%;
}
.formLabel {
  width: 80%;
  margin-top: 4%;
  font-size: 18px;
  letter-spacing: 1px;
  display: inline-block;
}
input {
  display: block;
  width: 90%;
  margin-top: 15px;
  height: 30px;
  font-size: 18px;
  color: gray;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #bec2c4;
  padding-left: 10px;
}
select {
  display: block;
  width: 90%;
  margin-top: 15px;
  font-size: 16px;
  color: gray;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #bec2c4;
  padding: 5px;
  letter-spacing: 1px;
}
.skills {
  margin-top: 20px;
  background-color: #bec2c4;
  display: inline-block;
  margin-left: 10px;
  padding: 7px 20px;
  border-radius: 20px;
  height: 40px;
  font-size: 20px;
  color: black;
  cursor: pointer;
}
.formCheck {
  display: flex;
  flex-direction: row;
  width: 80%;
  margin-top: 10px;
}
.formCheck input {
  margin-right: 15px;
  width: 20px;
}
.formCheck label {
  letter-spacing: 1px;
  text-transform: uppercase;
  font-size: 18px;
  margin-top: 20px;
}
button {
  width: 250px;
  margin-top: 40px;
  margin-left: 35%;
  height: 50px;
  border-radius: 25px;
  background-color: #6ea4e6;
  color: white;
  font-size: 20px;
  border: none;
  cursor: pointer;
}
.error {
  color: red;
  font-size: 20px;
  margin-top: 10px;
}
</style>