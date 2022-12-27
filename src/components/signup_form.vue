<template>
  <div class="formStart">
    <label class="formLabel">EMAIL:</label>
    <input type="email" required v-model="email" />

    <label class="formLabel">PASSWORD:</label>
    <input type="password" v-model="password" />
    <div v-if="passwordValidation" class="error">{{ passwordValidation }}</div>

    <label class="formLabel">ROLE:</label>
    <select v-model="role">
      <option value="">SELECT A ROLE</option>
      <option value="web Developer">WEB DEVELOPER</option>
      <option value="web Designer">WEB DESIGNER</option>
    </select>
    <label class="formLabel">SKILLS:</label>
    <input type="text" v-model="skillTemp" @keyup="addSkill" />
    <div class="skills" v-for="skill in skills" :key="skill">
      <div @click="deleteSkill(skill)">
        {{ skill }} <i class="fa-solid fa-circle-xmark"></i>
      </div>
    </div>
    <div class="formCheck">
      <input type="checkbox" v-model="term" />
      <label>accept terms and conditions</label>
    </div>
    <label class="formLabel error">{{ warning }}</label>
    <button @click.prevent="formSubmit">Create an account</button>
  </div>
  <div class="formDetails" :class="{ hidden: !formSubmitted }">
    <h1>Email: {{ email }}</h1>
    <h1>Password: {{ password }}</h1>
    <h1>Role: {{ role }}</h1>
    <div class="skillsDetail">
      <h1>Skills:</h1>
      <h1 v-for="skill in skills" :key="skill">{{ skill }}</h1>
    </div>
    <h1>Terms Accepted: {{ term }}</h1>
  </div>
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
      passwordReg: "",
      formSubmitted: false,
      warning: "",
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
      if (e.key === "Enter" && this.skillTemp) {
        if (!this.skills.includes(this.skillTemp)) {
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
      this.passwordReg = new RegExp(
        "(?=.*[a-z])(?=.*[A-Z])(?=.*[0-9])(?=.*[!@#$%^&*(),.?:{}|<>])"
      );
      if (this.email && this.role && this.term) {
        if (this.password.length < 8) {
          this.passwordValidation =
            "Password length should be more than 8 characters";
        } else if (!this.passwordReg.test(this.password)) {
          this.passwordValidation =
            "Password is not strong enough must contain a number upper,lower and special char";
        } else {
          this.passwordValidation = "";
          this.formSubmitted = true;
        }
        this.warning = "";
      } else {
        this.warning = "please fill all the above fields";
      }
    },
  },
};
</script>

<style scoped>
.formStart {
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
  margin-bottom: 40px;
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
.formDetails {
  margin-top: 20px;
  align-items: center;
  text-align: center;
}
.skillsDetail {
  display: block;
}
.skillsDetail h1 {
  display: inline-block;
  margin-left: 10px;
}
.hidden {
  display: none;
}
i {
  color: grey;
}
</style>