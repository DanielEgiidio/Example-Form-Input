<template>
  <form @submit.prevent="handleSumbit">
    <label>Email:</label>
    <input type="Email" required v-model ="email" placeholder="example@gmail.com">

    <label>Senha:</label>
    <input type="password" required v-model ="password" placeholder="********">
    <div v-if="passwordError" class="error">{{ passwordError }}</div>

    <label>Cargo:</label>
    <select v-model="role">
      <option value="frontend">Desenvolvedor FrontEnd</option>
      <option value="mobile">Desenvolvedor Mobile</option>
    </select>

    <label>Skills:</label>
    <input type="text" v-model="tempSkill" @keyup="addSkill" placeholder="Insira a skill e pressione Enter">
    <div v-for="skill in skills" :key="skill" class="pill">
      <span @click="deleteSkill(skill)">{{skill}}</span>
    </div>

    <div class="terms">
      <input type="checkbox" required v-model="terms" >
      <label>Termos e condições</label>
    </div>

    <div class="sumbit">
      <button>Criar Conta</button>
    </div>

  </form>


  <p>Email: {{ email }}</p>
  <p>Password: {{ password }}</p>
  <p>Role: {{ role }}</p>
  <p>Terms: {{ terms }}</p>
</template>

<script>
export default {
  data() {
    return {
      email: '',
      password: '',
      role: 'frontend',
      terms: false,
      tempSkill:'',
      skills: [],
      passwordError: ''
    }
  },
  methods: {
    addSkill(e) {
      if(e.key === "Enter" && this.tempSkill) {
        if(!this.skills.includes(this.tempSkill)){
          this.skills.push(this.tempSkill)
        }
        this.tempSkill = ""
      }
    },
    deleteSkill(skill){
      this.skills = this.skills.filter((item) => {
        return skill !== item;
      })
    },
    handleSumbit() {
      this.passwordError = this.password.length > 5 ?
      '' : 'Senha muito curta';

      if(!passwordError) {
        console.log('email: ', this.email);
        console.log('password: ', this.password);
        console.log('role: ', this.role);
        console.log('skills: ', this.skills);
        console.log('termos aceitos: ', this.terms);
      }
    }
  }
}
</script>

<style>
  
  form{
    max-width: 500px;
    margin: 30px auto;
    background: white;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
  }
  label {
    display:inline-block;
    color: #aaa;
    margin: 25px 0 15px;
    font-size: 0.6rem;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
    padding-right: 5px;
  }
  input, select {
    display: block;
    padding: 10px 0 10px;
    width: 100%;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
    box-sizing: border-box;
    font-size: 1rem; 
  }
  ::placeholder {
    color: #aaa;
  }
  :focus {
    outline: none
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
    font-style: 12px;
    letter-spacing: 1px;
    font-weight: bold;
    color: #777;
    cursor: pointer;
  } 
  button {
    background-color: #0b6dff;
    border: none;
    padding: 10px;
    width: 100%;
    margin-top: 20px;
    color: white;
    border-radius: 10px;
    cursor: pointer;
  }
  .submit {
    text-align: center;
  }
</style>