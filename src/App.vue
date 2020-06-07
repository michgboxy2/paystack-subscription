<template>
  <div id="app">
    <div class="container">
      <h4>Make Payment</h4>
      <div>
        <form class="payment-form">
          <label for="firstName">First Name</label>
          <input type="text" placeholder="First Name" v-model="firstName" required/>

          <label for="lastName">Last Name</label>
          <input type="text" placeholder="Last Name" v-model="lastName" required/>

          <label for="Email">Email Address</label>
          <input type="email" placeholder="Email Address" v-model="email" required/>
          
          <div>
              <button type="button" class="login-form-btn" @click="payWithPaystack">Pay</button>
          </div>

          <!-- <script src="https://js.paystack.co/v1/inline.js"></script> -->
        </form>
      </div>
    </div>
 
  </div>
</template>

<script>


export default {
  name: 'App',
  components: {
    
  },
  data() {
    return {
      firstName: '',
      lastName: '',
      email: '',
    }
  },
  methods: {
    click(){
    },
    
    payWithPaystack(){
      if(!this.firstName || !this.lastName || !this.email){
        alert("Kindly fill up all fields");
        return;
      }
    var handler = window.PaystackPop.setup({
      key: 'pk_test_c54848d605d7b76297b0ef18492bbb1dd7ad7fbd',
      email: this.email,
      plan: "PLN_ns8lsw89s1z4vzz",
      ref: ''+Math.floor((Math.random() * 1000000000) + 1),
      metadata: {
         custom_fields: [
            {
                display_name: this.firstName,
                lastName: this.lastName,
                email: this.email,
                firstName: this.firstName,
                variable_name: 'email',
                value: this.email
            }
         ]
      },
      callback: function(response){
          alert('successfully subscribed. transaction ref is ' + response.reference);
      },
      onClose: function(){
          alert('window closed');
      }
    });
    handler.openIframe();
  }
  }
}
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

html {
    /* 10px /16px = .625 * 100.     //make 10px = 1rem*/
    font-size: 62.5%;
}

body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}

h4 {
  margin: 70px auto;
  color: #27a8b4;
  font-size: 3rem;
  font-weight: bold;

}

.container {
  width: 100%;
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.payment-form {
  background-color: #f8f9fa;
  padding: 1rem;
  height: 40rem;
  width: 40rem;
}

.payment-form label {
    font-size: 1.2rem;
    font-weight: bold;
    margin-left: 1.5rem;
    margin-bottom: 1rem;
}

.payment-form input {
  width: 35rem;
  height: 3.5rem;
  padding-left: 1rem;
  font-size: 1.2rem;
  font-weight: 400;
  margin-bottom: 1.5rem;
  border: 0.1rem solid #ddd;
  border-radius: 0.5rem;
  transition: background-color 0.3s;
  margin-left: 1.5rem;
  outline: none;
}

.payment-form input:focus {
  background-color: #d9ebf7;
}

.payment-form button {
    padding: 1rem 1.5rem;
    background-color: #28a745;
    color: #fff;
    border-radius: 0.5rem;
    cursor: pointer;
    font-size: 1.5rem;
    font-weight: 300;
    margin: 2rem 4rem;
    width: 30rem;
    transition: background-color 0.3s;
    outline: none;
}

.payment-form button:hover {
  background-color:	#2E8B57;
}

/* #1af5d1; */


</style>
