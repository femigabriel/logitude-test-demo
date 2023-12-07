<template>
  <div class="app">
    <link
      rel="stylesheet"
      href="https://use.fontawesome.com/releases/v5.15.4/css/all.css"
      integrity="sha384-DyZ88mC6Up2uqS4h/KRgHuoeGwBcD4Ng9SiP4dIRy0EXTlnuz47vAwmeGwVChigm"
      crossorigin="anonymous"
    />

    <div>
      <div class="logo">
        <NuxtLink to="/about">
          <img
            id="loginlogo"
            style="margin-top: 50px; width: 290px; height: 114px"
            src="../../images/LogitudeLogo.jpg"
          />
        </NuxtLink>
      </div>
      <img src="../../images/shadow1.png" alt="" />
      <div class="container">
        <form
          action="https://httpbin.org/post"
          method="POST"
          class="form login"
          novalidate="true"
          v-on:submit.prevent="validate"
          autocomplete="off"
          id="Form"
        >
          <div class="form-group">
            <div class="form-field">
              <label for="">e-mail:</label>
              <div class="form-input">
                <input
                  name="Email"
                  type="email"
                  v-bind:class="{
                    'is-valid': validation.valid.email,
                    'is-invalid': validation.invalid.email,
                  }"
                  v-on:focus="clearValidation('email')"
                  v-model="email"
                  autocomplete="on"
                  placeholder="e.g. myname@example.net"
                  class="input"
                  onblur="onEmailBlur()"
                  style="width: 258px; padding: 5px 10px; height: 33px"
                  size="10"
                  required
                  pattern="^\S+@\S+\.\S+$"
                  data-email-msg="Email format is not valid"
                />
              </div>

              <span class="error-message" v-if="validation.invalid.email">
                {{ validation.invalid.email }}
              </span>
            </div>
            <div class="form-field">
              <label for="">Password:</label>
              <div class="form-input">
                <input
                  name="Password"
                  type="text"
                  v-if="showPassword"
                  v-bind:class="{
                    'is-valid': validation.valid.password,
                    'is-invalid': validation.invalid.password,
                  }"
                  v-on:focus="clearValidation('password')"
                  v-model="password"
                  class="input"
                  style="width: 230px; padding: 5px 10px; height: 33px"
                  autocomplete="off"
                  oninput="onPasswordChanged()"
                  data-email-msg="password is required!"
                  onkeypress="capLock(event)"
                  required
                  :type="passwordFieldType"
                />
                <input
                  v-else
                  type="password"
                  class="input"
                  style="width: 230px; padding: 5px 10px; height: 33px"
                  v-model="password"
                />
                <div class="btn-eyes" @click="toggleShow">
           
                  <i
                    class="fas eyes"
                    :class="{
                      'fa-eye-slash': showPassword,
                      'fa-eye': !showPassword,
                    }"
                  ></i>
                </div>
              </div>
              <!-- <span class="valid-feedback" v-if="validation.valid.password">
                {{ validation.valid.password }}
              </span> -->

              <span class="error-message" v-if="validation.invalid.password">
                {{ validation.invalid.password }}
              </span>
            </div>

            <div class="action-btn">
              <button class="login-btn" type="submit">Login ></button>
              <NuxtLink to="/about">
                <a href="/">Forgot your password?</a>
              </NuxtLink>
            </div>
          </div>
        </form>
        <div class="layer">
          <img
            id="DirectlyLayerImage"
            width="650"
            style="
              display: inline;
              /* height: 260px; */
              min-width: 650px;
              width: 650px;
              border: 0px;
            "
            src="../../images/Layer.png"
            draggable="false"
          />
        </div>
      </div>
      <img src="../../images/shadow2.png" alt="" />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      firstName: "",
      showPassword: false,
      password: null,
      validation: {
        invalid: {},
        valid: {},
      },
    };
  },
  computed: {
    buttonLabel() {
      return this.showPassword ? "Hide" : "Show";
    },
  },
  methods: {
    validate: function () {
      if (!this.email) {
        this.validation.invalid.email = "Please enter your email.";
      } else if (this.email.length < 2) {
        this.validation.invalid.email =
          "username should have min. 2 characters.";
      } else {
        this.validation.valid.email = "";
      }
      if (!this.password) {
        this.validation.invalid.password = "Please enter password.";
      } else if (this.password.length < 8) {
        this.validation.invalid.password =
          "Password should have min. 8 characters.";
      } else if (this.password.match(/[^a-z]/i)) {
        this.validation.invalid.password =
          "Password should contains only latin letters (a-z).";
      } else {
        this.validation.valid.password = "Password is strong.";
      }

      this.$forceUpdate();
    },
    toggleShow() {
      this.showPassword = !this.showPassword;
    },
  },

  clearValidation: function (field) {
    this.validation.valid[field] = "";
    this.validation.invalid[field] = "";
    this.$forceUpdate();
  },
};
</script>

<style>
@import url("https://fonts.cdnfonts.com/css/lucida-sans-unicode");

.app {
  width: 100%;
  margin-top: 10px;
  display: flex;
  justify-content: center;
}

.logo {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 80px;
}
.container {
  width: 100%;
  display: flex;
  background: #fff;
  padding: 20px 10px;
  padding-bottom: 0px;
  /* box-shadow: 0px 2px 2px #888, 0px -2px 2px #888; */
  /* margin-top: 80px; */
  padding-right: 0;
}

.form-group {
  padding: 20px;
  background: #fff;
  padding-right: 80px;
}
.form-field {
  display: flex;
  flex-direction: column;
  margin: 10px 0;
}
.form-input {
  /* height: 33px;
  width: 267px; */
  border: 1px solid #d1d1d1;
  background: url(../../images/input.svg);
  background-position: center;
  background-repeat: no-repeat;
  border-radius: 4px;
  color: #45494a;
  border-radius: 3px;
  display: flex;
}
input {
  background: url(../../images/input.svg);
  border-radius: 3px;
  height: 33px;
  box-shadow: inset 0 0 10px #d1d1d1;
}
input:focus {
  outline: none;
  border: none;
}
.btn-eyes {
  border-radius: 3px;
  padding: 0 5px;
}
.form-input .eyes {
  margin-top: 8px;
  width: 20px;
  height: 18px;
  cursor: pointer;
}
.action-btn {
  display: flex;
  justify-content: space-between;
  width: 100%;
  margin-top: 20px;
}
.action-btn a {
  margin-left: 15px;
  margin-top: 10px;
  color: #4b4a4a;
  font-size: 12px;
  font-family: Arial;
  cursor: pointer;
}
.login-btn {
  background-color: #fe1a00;
  -webkit-border-radius: 6px;
  border-radius: 6px;
  border: 1px solid #d83526;
  display: inline-block;
  color: #ffffff;
  font-family: arial;
  font-size: 15px;
  font-weight: bold;
  padding: 6px 24px;
  text-decoration: none;
  text-shadow: 1px 1px 0px #b03466;
  /* width: 100px; */
}
.layer {
  /* border-left: 1px solid darkgrey; */
  width: 100%;
}
.error-message {
  color: #fe1a00;
  font-size: 12px;
}
</style>
