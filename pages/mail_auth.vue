<template>
  <div id="mail-wrap">
    <div class="container">
      <div id="mail-h">
        <p> メール でログイン</p>
      </div>
      <form action="/" method="post" v-on:submit.prevent="on_submitted">
        <div class="form-item" v-if="sign_type">
          <!-- <label for="name-place">ユーザー名</label> -->
          <input type="text" id="name-place" name="user-name" placeholder="ユーザー名" v-model="user_name">
        </div>
        <div class="form-item">
          <!-- <label for="mail-place">メール</label> -->
          <input type="email" id="mail-place" name="user-email" placeholder="メール" v-model="mail_addr">
        </div>
        <div class="form-item">
          <!-- <label for="pass-place">パスワード</label> -->
          <input type="password" id="pass-place" name="user-pass" minlength="6" placeholder="パスワード" v-model="password">
        </div>
        <div class="form-submit">
          <input v-if="!sign_type" type="submit" value="LOGIN">
          <input v-else type="submit" value="SIGNUP">
        </div>
        <div class="form-item">
          <p v-if="!sign_type">アカウントを持っていませんか？<a href="#" v-on:click="change_type">SIGNUP</a></p>
          <p v-else>アカウントを持っています <a href="#" v-on:click="change_type">SIGNIN</a></p>
        </div>
      </form>
    </div>
  </div>
</template>


<script>
  import firebase from '~/plugins/firebase_auth.js';

  const axios = require('axios');

  export default {
    components: {
      firebase,
    },
    data: function () {
      return {
        user_name: '',
        mail_addr: '',
        password: '',
        sign_type: false,
      };
    },
    created: function () {},
    methods: {
      on_submitted: function (event) {
        if (this.sign_type) {
          if (!this.user_name == '') {
            firebase.signup(this.$store, this.user_name, this.mail_addr, this.password);
          } else {
            alert("the length of username should be more than 5 chars.\nor type of password is int.")
          }
        } else {
          firebase.login(this.$store, this.mail_addr, this.password);
        }
      },
      change_type: function () {
        this.sign_type = !this.sign_type;
      }
    }
  }
</script>

<style scoped>
  #mail-wrap {
    /* background: #0004de; */
    height: 500px;
    margin-bottom: 100px;
  }

  #mail-h {
    /* background: red; */
    /* display: flex;
    justify-content: center;
    text-align: center; */
    width: 100%;
    margin: 0 auto;
    /* border-bottom: solid 1px gray; */
    border-bottom: 1px solid;
    border-image: linear-gradient(to right, #0004de 0%, #bd5aac 100%);
    border-image-slice: 1;
  }

  #mail-h p {
    font-size: 2.5vw;
    font-family: cursive;

  }

  .container {
    /* background: #af7272; */
    display: flex;
    justify-content: center;
    text-align: center;
    /* position: fixed; */
    width: 60vw;
    height: 30vw;
    position: absolute;
    display: flex;
    flex-direction: column;
    left: 50%;
    top: 45%;
    transform: translate(-50%, -50%);
    /* height: 100%; */
    /* background: linear-gradient(to left, #333,#eee); */
  }

  .container form {
    /* background: rgb(197, 188, 108); */
    height: 27vw;
    vertical-align: center;
    margin-top: 2%;
    width: 70%;
    margin: 0 auto;
  }

  .form-item input {
    width: 100%;
    font-size: 1.2em;
    line-height: 30px;
    background: #fbfbfb;
    outline: none;
    border: none;
    border-bottom: solid 2px #0984e3;
    text-align: center;
    transition: .3s;
  }

  .form-item {
    position: relative;
    margin: 2.2em 0em;
    padding: 5px;
  }

  .form-item:hover input {
    /* box-shadow: 1px 1px 1px 1px gray; */
    border-bottom: solid 2px #a24fc3;
    transition: .3s;
  }

  .form-submit {
    /* background: #bd5aac; */
    display: inline-block;
  }

  .form-submit input {
    border-radius: 2px;
    box-shadow: 0 1px 0 rgba(0, 0, 0, 0.05);
    box-sizing: border-box;
    transition: all .2s;
    background-color: #0984e3;
    border: 1px solid #b2bec3;
    color: #dfe6e9;
    cursor: pointer;
    border-radius: 4px;
    display: inline-block;
    font-size: 0.8em;
    font-style: normal;
    font-weight: 500;
    height: 36px;
    line-height: 34px;
    min-width: 40px;
    padding: 0 3em;
    /* margin: 10px; */
    position: relative;
    text-align: center;
    text-decoration: none;
    white-space: nowrap;
    vertical-align: middle
  }

  .form-submit:hover input {
    background-color: #8cc2ec;
  }

  /* @media screen and (min-width: 501px) {
    form {
      position: absolute;
      display: flex;
      flex-direction: column;
      left: 50%;
      top: 50%;
      transform: translate(-50%, -50%);
      color: #2d3436;
      text-align: center;
    }

    form {
      background: #dfe6e9;
      margin: 0px;
      padding: 20px;
      min-width: 400px;
      max-width: 600px;
      width: 50%;
      height: auto;
      border: solid 1px #dfe6e9;
      box-shadow: 5px 5px 4px;
      border-radius: 30px;
    }

    .form-item input {
      width: 80%;
      font-size: 25px;
      line-height: 30px;
      background: #dfe6e9;
      outline: none;
      border: none;
      border-bottom: solid 1px #0984e3;
      text-align: center;
    }
  } */

  /*

@media screen and (max-width: 500px) {
  .container {
    background: #dfe6e9;

  }

  form {
    width: 100%;
    height: auto;
    background: #dfe6e9;
  }

  .form-item input {
    width: 100%;
    font-size: 25px;
    line-height: 30px;
    background: #dfe6e9;
    outline: none;
    border: none;
    border-bottom: solid 1px #0984e3;
    text-align: center;
  }
} */

  /* .form-item {
    position: relative;
    margin: 10px 20px;
    padding: 5px;
  } */


  /* .form-submit input {
    border-radius: 2px;
    box-shadow: 0 1px 0 rgba(0, 0, 0, 0.05);
    box-sizing: border-box;
    transition: all .2s;
    background-color: #0984e3;
    border: 1px solid #b2bec3;
    color: #dfe6e9;
    cursor: pointer;
    display: inline-block;
    font-size: 14px;
    font-style: normal;
    font-weight: 500;
    height: 36px;
    line-height: 34px;
    min-width: 40px;
    padding: 0 20px;
    margin: 10px;
    position: relative;
    text-align: center;
    text-decoration: none;
    white-space: nowrap;
    vertical-align: middle
  } */
</style>