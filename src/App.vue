<template>
  <section class="container">
    <!-- <h2>{{ userName }}</h2>
    <h3>{{ age }}</h3>
    <p>{{ user }}</p> -->

    <user-data :first-name="firstName" :last-name="lastName" :age="age"></user-data>
    <button @click="setAge">Change Age</button>

    <!-- <h2>{{user.name}}</h2>
    <h3>{{user.age}}</h3>
    <button @click="setAge">Change Age</button> -->

    <!-- <div>
      <input type="text" placeholder="First Name" @input="setFirstName" />
      <input type="text" placeholder="Last Name" @input="setLastName" />
    </div> -->

    <div>
      <input type="text" placeholder="First Name" v-model="firstName" />
      <input type="text" placeholder="Last Name" ref="lastNameInput" />
      <button @click="setLastName">Set Name</button>
    </div>
  </section>
</template>

<script>
import { ref, computed, watch, provide } from 'vue';
// import { reactive } from 'vue';
import UserData from './components/UserData.vue';

export default {
  components: {
    UserData
  },
  setup() { 
    const firstName = ref('');
    const lastName = ref('');
    const uAge = ref(22);

    const lastNameInput = ref(null);

    /* const user = reactive({ // ref => ref
      name: 'Amanda',
      age: 22,
    }); */

    provide('userAge',uAge);
    
    const uName = computed(function() {
      return firstName.value + ' ' + lastName.value;
    });

     watch([uAge, uName], function(newValue, oldValue) {
      console.log("Old Age " + oldValue[0]);
      console.log("New Age " + newValue[0]);

      console.log("Old Name " + oldValue[1]);
      console.log("New Name " + newValue[1]);
    });

    /* const uName = ref('Amanda');*/

    /* setTimeout(function(){
      // uName.value = 'An Egg',
      // uAge.value = 23
      
      // user.value.name = 'An Egg',
      // user.value.age = 23
      user.name = 'An Egg',
      user.age = 23
    },2000);*/

    /* return { 
      userName: uName,
      age: uAge
    }; */

    /* return { 
        userName: user.value.name,
        age: user.value.age,
        user: user
    }*/

    function setNewAge(){
      // user.age  = 32;
      uAge.value = 23;
    }

    function setLastName(){
      lastName.value = lastNameInput.value.value;
    }

    // function setFirstName(event){
    //   firstName.value = event.target.value;
    // }

    // function setLastName(event){
    //   lastName.value = event.target.value;
    //}

    // return {user:user , setAge: setNewAge}
    // return { setFirstName, setLastName}
    return { 
      userName : uName,
      age: uAge,
      setAge: setNewAge ,
      firstName: firstName,
      lastName,
      lastNameInput,
      setLastName}
  },
  /* data() {
    return {
      userName: 'Amanda',
    };
  },*/
  // provide(){
  //   return { age: this.age }
  // }
};
</script>

<style>
* {
  box-sizing: border-box;
}

html {
  font-family: sans-serif;
}

body {
  margin: 0;
}

.container {
  margin: 3rem auto;
  max-width: 30rem;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 1rem;
  text-align: center;
}
</style>