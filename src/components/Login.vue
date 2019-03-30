<template>
 <div>
   <form class="login" @submit.prevent="login">
     <h1>Sign in</h1>
     <label>Email</label>
     <input required v-model="email" type="email" placeholder="Email"/>
     <label>Password</label>
     <input required v-model="password" type="password" placeholder="Password"/>
     <hr/>
     <button type="submit">Login</button>
     <br/>
     <div>{{authStatus}}</div>
   </form>
 </div>
</template>

<script>
  export default {
    data(){
      return {
        email : "",
        password : ""
      }
    },
    computed: {
    	authStatus() {
    		console.log(this.$store.getters.authStatus);
    		return this.$store.getters.authStatus;
    	}
    },
    methods: {
      login: function () {
        let email = this.email 
        let password = this.password
        this.$store.dispatch('login', { user: { email, password } })
       		.then(() => this.$router.push('/'))
       		.catch(err => console.log(err))
      }
    }
  }
</script>