# Vuex

### You have to just follow a few steps to get following Vuex services


## Getting Started
### Step 1: install this npm package

```` 
npm install vuex --save

````

## Step 2:Import Vuex on js/store/index.js.

````
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

````
## Step 3:write on index.js.

````
import Vue from 'vue';
import Vuex from 'vuex'
Vue.use(Vuex)

const store = new Vuex.Store({
    state: {
      massage:"Welcome, People",
      user:[],
    },
    getters: {
      getMassage(state){
          return state.massage;
      },
      getUser(state){
        return state.user;
      }
    },
    mutations:{
        SET_USER(state, data){
            state.user = data;
        }
    }
  })

export default store;

// state data seen to using getters and also using getMassage() function

// mutations set data into state and then this data return on getters function;

````
### Step 4: import this stroe folder on app.js and use 

```` 
import store from './store/index'

``
const app = new Vue({
    el: '#app',
    router:routes,
    store,
});
```` 
### Step 5: set mutation function value use getUserData function on auth/login.vue

```` 
methods:{
        login(){
            axios.get('/sanctum/csrf-cookie').then(response => {
                this.loginForm.post('/login').then(response =>{
                      
                     //call getUserData function for user data
                     this.getUserData();
                    this.$router.push({name:'dashboard'});

                }); 
            });
        },

        getUserData(){
            axios.get('/api/user').then(response =>{
                let user = response.data;
                //set user data on mutations in index.js file
                this.$store.commit('SET_USER', user)
            });
        },
    },
    
```` 

### Step 6: Output where we want to see our data/ dashboard/index.js

```` 
<template>
  <h5>{{massage}}</h5>
  <h5>Welcome to Dashboard,Mr {{user.name}}</h5>
</template>
<script>
export default {
    computed:{
        massage(){
            return this.$store.getters.getMassage;
        },
        user(){
            return this.$store.getters.getUser;
        }
    }
}
    
```` 




















