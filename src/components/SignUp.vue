<template>
  <form @submit.prevent="handleSubmitEvent">
    <label>Email :</label>
    <input type="email" required v-model="email" />

    <label>Password :</label>
    <input type="password" required v-model="password" />
     <span class="error"> {{passwordCheck}}</span>
    <label>Role:</label>
    <select v-model="role">
      <option value="Designer">Web Designer</option>
      <option value="Developer">Web Developer</option>
    </select>

    <label >Add your skills </label>
    <input type="text" v-model="tempSkill" @keyup.alt="addSkill" placeholder="press alt + , to add new skill"> <!-- alt + (,) to does not show comma in the screen   -->
    <div v-for="skill in skills" :key="skill" class="pill"> <!--  -->
        <p @click="removeItem(skill)"> {{skill}}</p>
    </div>

    <p>Choose book or books</p>
    <div class="terms">
      <input type="checkbox" value="Moby Dick" v-model="names" />
      <label>Moby Dick</label>
    </div>
    <div class="terms">
      <input type="checkbox" value="Anna Kararinna" v-model="names" />
      <label>Anna Kararinna</label>
    </div>
    <div class="terms">
      <input type="checkbox" value="White Nights" v-model="names" />
      <label>White Nights</label>
    </div>

    <div class="terms">
      <input type="checkbox" v-model="terms" />
      <label>Accept Terms and Conditions </label>
    </div>
    
    <div class="submit">
      <button>Save</button>
    </div>
  </form>
  <p>E-mail : {{ email }}</p>
  <p>Password : {{ password }}</p>
  <p>Role : {{ role }}</p>
  <p>Skills : {{skills}}</p>
  <p>Terms Accepted : {{ terms }}</p> 
  <p>Names :{{ names }}</p>
</template>
<!-- 
two ways data binding(v-model:data) : when we input values to email , it updates email property in data function in the same time 
and if we updates email property in data() function , email updates in the template one at the same time 
 -->
<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "Designer",
      terms: false,
      names: [],
      tempSkill:"",
      skills:[],
      removeSkill:[],
      passwordCheck:'',
    };
  },
  methods:{
    addSkill(keyEvent){
    
       if(keyEvent.key===',' && this.tempSkill){ // (,) girilmişse ve tempSkill boş değil ise 
        //to avoid reply same skill in the arraylist 
        if(!this.skills.includes(this.tempSkill)){
            this.skills.push(this.tempSkill);
        }
            this.tempSkill='';
            this.displaySkill =true;
       }
    },
    removeItem(skill){
       this.skills = this.skills.filter((arrayItem)=>{
         return skill !== arrayItem;
       })
    },
    handleSubmitEvent(){ //but we want to prevent default submit event action 
      this.passwordCheck = this.password.length > 5 ? '' : 'Password must be at least 5 character long';
    }
  }
};
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
input,
select {
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
}
input[type="checkBox"] {
  display: inline-block;
  width: 16px;
  margin: 0 10px 0 0;
  position: relative;
  top: 2px;
}
.pill{
  display: inline-block;
  margin: 20px 10px 0 0 ;
  padding: 6px 12px;
  background: #eee;
  border-radius: 20px;
  font-size: 12px;
  letter-spacing: 1px;
  font-weight: bold;
  color: #777;
  cursor: pointer;
}
.submit{
   text-align: center;
}

button{
   background: #0b6dff;
   border: 0;
   padding: 10px 20px;
   margin-top: 20px;
   color: white;
   border-radius:20px ;
}
.error{
  color: rgb(150, 37, 37);
  margin: 10px auto 5px auto;
  font-weight: bold;
  display: block;
  font-size: 12px;
}
</style>