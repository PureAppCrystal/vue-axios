<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div id="state">
      <p> Login 상태 : {{logined ? "로그인" : "로그아웃"}} </p>
      
      <button v-on:click="login"> Login </button>
      <button v-on:click="logout"> Logout </button>
    </div>

    
    <div id="request" >
      <p> 요청결과 : {{ request ? "성공" : "실패"}} </p>
      <p> {{message}} </p>
      <button v-on:click="guest"> Guest </button>
      <button v-on:click="member"> member </button>
      <button v-on:click="manager"> manager </button>
      <button v-on:click="admin"> admin </button>
    </div>
    
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data: () => {
    return {
      logined: false,
      request: false,
      message: "hello",

    }
  },
  methods: {
    login: function () {
      console.log("====== Login ====== ")
      //test
      let form = new FormData();
      form.append("username", "manager");
      form.append("password", "manager");
      console.log("form : ", form)

      let data = {
        username: "manager",
        password: "manager"
      }
      console.log("data : ", data)

      axios.post("http://localhost:8000/api/login" , data)
        .then(res => {
          console.log("res : ", res);
          this.message = res;
          return this.request = true;
        })
        .catch( e=> {
          console.log("err : ", e)
          this.message = e;
        })
    },
    logout: function() {
      console.log("====== Logout ====== ")
          axios.post("http://localhost:8000/logout" , {
        user: 'admin',
        password: '1234'
      })
        .then(res => {
          console.log("res : ", res);
          this.message = res;
          return this.request = true;
        })
        .catch( e=> {
          console.log("err : ", e)
          this.message = e;
        })
    },
    guest: function() {
      console.log("====== Guest ====== ")
      axios.get("http://localhost:8000/api/guest")
        .then(res => {
          console.log("res : ", res);
          this.message = res;
          return this.request = true;
        })
        .catch( e=> {
          console.log("err : ", e)
          this.message = e;
        })
        
    },  
    member: function() {
      console.log("====== member ====== ")
      axios.get("http://localhost:8000/api/member")
        .then(res => {
          console.log("res : ", res);
          this.message = res;
        }).catch( e=> {
          console.log("err : ", e)
          this.message = e;
        })
        
    },
    manager: function() {
      console.log("====== manager ====== ")
      axios.get("http://localhost:8000/api/manager")
        .then(res => {
          console.log("res : ", res);
          this.message = res;
        }).catch( e=> {
          console.log("err : ", e)
          this.message = e;
        })
        
    },
    admin: function() {
      console.log("====== admin ====== ")
      axios.get("http://localhost:8000/api/admin")
        .then(res => {
          console.log("res : ", res);
          this.message = res;
        }).catch( e=> {
          console.log("err : ", e)
          this.message = e;
        })
        
    },
    
  },
  created () {
    console.log("====== HelloWorld created ======")
    // axios.get("http://localhost:8000/api/guest")
    //   .then(res => {
    //     console.log("res : ", res);
    //     this.message = res;
    //   })
      
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}


#state {
  margin: 1rem;
}

#request {
  margin: 1rem;
}
</style>
