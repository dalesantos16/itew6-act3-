<template>
    <div class="login-container">
      <h1>Login</h1>
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
        // Simulate generating a random token
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
    margin: 0 auto;
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 8px;
    background-color: #f9f9f9;
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
    width: 100%;
    padding: 8px;
    border: 1px solid #ccc;
    border-radius: 4px;
  }
  
  button.login-btn {
    font-family: Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
    width: 100%;
    padding: 10px;
    border: none;
    border-radius: 4px;
    background-color: #007bff;
    color: #fff;
    cursor: pointer;
    transition: background-color 0.3s;
  }
  
  button.login-btn:hover {
    font-family: Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
    background-color: #0056b3;
  }
  </style>
  