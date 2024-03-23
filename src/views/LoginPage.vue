<template>
    <div class="login-container">
      <h1>Log In Your Account</h1>
      <form @submit.prevent="handleLogin" class="login-form">
        <div class="form-group">
          <label style="font-family:Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif" for="email">Email:</label>
          <input type="email" id="email" v-model="email" required>
        </div>
        <div class="form-group">
          <label style="font-family:Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif" for="password">Password:</label>
          <input type="password" id="password" v-model="password" required>
        </div>
        <button type="submit" class="login-btn">Login</button>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        email: '',
        password: ''
      };
    },
    methods: {
      handleLogin() {
        const token = Math.random().toString(36).substr(2);
        localStorage.setItem('token', token);
        this.$router.push({ name: 'cartApp' });
      }
    }
  };
  </script>
  
  <style scoped>

  .login-container {
    max-width: 400px;
    margin: auto;
    padding: 60px;
    border: 3px solid #131212;
    border-radius: 8px;
    background-color: #f9f9f9;
    background: linear-gradient(gray, white);
    box-shadow: 10px 10px 4px 0 rgba(0, 0, 0, 0.5);

  }
  
  h1 {
    font-family: Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
    text-align: left;
  }
  
  .login-form {
    
    display: flex;
    flex-direction: column;
  }
  .div{
    font-family: Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
  }
  
  .form-group {
    margin-bottom: 20px;
  }
  
  label {
    font-weight: bold;
  }
  
  input[type="email"],
  input[type="password"] {
    font-family: Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
    width: 100%;
    padding: 8px;
    border: 1px solid #ccc;
    border-radius: 4px;
    box-shadow: 2px 2px 4px 0 rgba(0, 0, 0, 0.5);
  }
  
  button.login-btn {
    font-size: 30px;
    font-family: Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
    width: 100%;
    padding: 10px;
    border: none;
    border-radius: 4px;
    background-color: #007bff;
    color: #fff;
    cursor: pointer;
    margin: 0 10px;
    transition: 0.3s;
    box-shadow: 2px 2px 10px 0px rgba(0, 0, 0.5);
  }
  
  button.login-btn:hover {
    font-family: Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
    background-color: #0056b3;
  }
  #password:hover , #email:hover{
    background-color: #d3d5d8;
  }
  </style>
  