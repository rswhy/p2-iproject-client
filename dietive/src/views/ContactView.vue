<script>
import { useFoodStore } from "@/stores/food";
import { mapActions, mapWritableState } from "pinia";

export default {
  data() {
    return {
      emailUser: "",
      subject: "",
      message: "",
    };
  },
  computed: {
    ...mapWritableState(useFoodStore, ["isLogin"]),
  },
  methods: {
    ...mapActions(useFoodStore, ["contactUsAction"]),
    async contactUsClick() {
      try {
        let payload = {
          emailUser: this.emailUser,
          subject: this.subject,
          message: this.message,
        };
        await this.contactUsAction(payload);
        this.$router.push("/");
      } catch (err) {
        const error = err.response.statusText;
        swal("Error", error, "error");
      }
    },
  },
  async created() {
    try {
      const token = localStorage.getItem("access_token");
      if (token) {
        this.isLogin = true;
      } else {
        this.isLogin = false;
      }
    } catch (err) {
      const error = err.response.statusText;
      swal("Error", error, "error");
    }
  },
};
</script>

<template>
  <div class="wrapper fadeInDown">
    <br />
    <div id="formContent">
      <!-- Tabs Titles -->

      <br /><br />
      <!-- Icon -->
      <div class="fadeIn first logo">
        <img
          style="width: 110px"
          src="../assets/Diet.jpg"
          id="icon"
          alt="User Icon"
        />
      </div>
      <br />
      <hr style="height: 1px; background-color: #ccc; border: none" />

      <h2 style="color: forestgreen">CONTACT US</h2>
      <br /><br />

      <!-- Login Form -->
      <form>
        <input
          type="text"
          id="login"
          class="fadeIn second"
          name="login"
          v-model="emailUser"
          placeholder="email / name"
        /><br /><br />
        <input
          type="text"
          id="password"
          class="fadeIn third"
          name="login"
          v-model="subject"
          placeholder="subject"
        /><br /><br />
        <textarea
          type="text"
          id="password"
          class="fadeIn third"
          name="login"
          cols="50"
          rows="10"
          v-model="message"
          placeholder="type your message..."
        /><br /><br />
        <input
          @click.prevent="contactUsClick"
          type="submit"
          class="fadeIn fourth"
          value="SEND EMAIL"
        />
      </form>

      <!-- <div id="formFooter">
        <p>
          Don't have any account ?
          <RouterLink to="/register" class="underlineHover" href="#"> Sign Up</RouterLink>
        </p>
      </div> -->
    </div>
    <br />
  </div>
</template>

<style scoped>
@import url("https://fonts.googleapis.com/css?family=Poppins");

/* BASIC */

html {
  background-color: #1ec041;
}

body {
  font-family: "Poppins", sans-serif;
  height: 100vh;
}

a {
  color: #3ba837;
  display: inline-block;
  text-decoration: none;
  font-weight: 400;
}

h2 {
  text-align: center;
  font-size: 16px;
  font-weight: 600;
  text-transform: uppercase;
  display: inline-block;
  margin: 40px 8px 10px 8px;
  color: #cccccc;
}

/* STRUCTURE */

.wrapper {
  display: flex;
  align-items: center;
  flex-direction: column;
  justify-content: center;
  width: 100%;
  min-height: 100%;
  padding: 20px;
}

.logo {
  display: flex;
  text-align: center;
  justify-content: center;
  width: 100%;
  object-fit: cover;
}

#icon {
  width: 40px;
}

#formContent {
  -webkit-border-radius: 10px 10px 10px 10px;
  border-radius: 10px 10px 10px 10px;
  background: #fff;
  padding: 30px;
  width: 90%;
  max-width: 800px;
  position: relative;
  padding: 0px;
  -webkit-box-shadow: 0 30px 60px 0 rgba(0, 0, 0, 0.3);
  box-shadow: 0 30px 60px 0 rgba(0, 0, 0, 0.3);
  text-align: center;
}

#formFooter {
  background-color: #f6f6f6;
  border-top: 1px solid #dce8f1;
  padding: 25px;
  text-align: center;
  -webkit-border-radius: 0 0 10px 10px;
  border-radius: 0 0 10px 10px;
}

/* TABS */

h2.inactive {
  color: #cccccc;
}

h2.active {
  color: #0d0d0d;
  border-bottom: 2px solid #3ad135;
}

/* FORM TYPOGRAPHY*/

input[type="button"],
input[type="submit"],
input[type="reset"] {
  background-color: #3ba837;
  border: none;
  color: white;
  padding: 15px 80px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  text-transform: uppercase;
  font-size: 13px;
  -webkit-box-shadow: 0 10px 30px 0 rgba(95, 186, 233, 0.4);
  box-shadow: 0 10px 30px 0 rgba(95, 186, 233, 0.4);
  -webkit-border-radius: 5px 5px 5px 5px;
  border-radius: 5px 5px 5px 5px;
  margin: 5px 20px 40px 20px;
  -webkit-transition: all 0.3s ease-in-out;
  -moz-transition: all 0.3s ease-in-out;
  -ms-transition: all 0.3s ease-in-out;
  -o-transition: all 0.3s ease-in-out;
  transition: all 0.3s ease-in-out;
}

input[type="button"]:hover,
input[type="submit"]:hover,
input[type="reset"]:hover {
  background-color: #3ad135;
}

input[type="button"]:active,
input[type="submit"]:active,
input[type="reset"]:active {
  -moz-transform: scale(0.95);
  -webkit-transform: scale(0.95);
  -o-transform: scale(0.95);
  -ms-transform: scale(0.95);
  transform: scale(0.95);
}

input[type="text"] {
  background-color: #f6f6f6;
  border: none;
  color: #0d0d0d;
  padding: 15px 32px;
  text-align: left;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 5px;
  width: 85%;
  border: 2px solid #f6f6f6;
  -webkit-transition: all 0.5s ease-in-out;
  -moz-transition: all 0.5s ease-in-out;
  -ms-transition: all 0.5s ease-in-out;
  -o-transition: all 0.5s ease-in-out;
  transition: all 0.5s ease-in-out;
  -webkit-border-radius: 5px 5px 5px 5px;
  border-radius: 5px 5px 5px 5px;
}

input[type="text"]:focus {
  background-color: #fff;
  border-bottom: 2px solid #3ad135;
}

input[type="text"]:placeholder {
  color: #cccccc;
}

input[type="password"] {
  background-color: #f6f6f6;
  border: none;
  color: #0d0d0d;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 5px;
  width: 85%;
  border: 2px solid #f6f6f6;
  -webkit-transition: all 0.5s ease-in-out;
  -moz-transition: all 0.5s ease-in-out;
  -ms-transition: all 0.5s ease-in-out;
  -o-transition: all 0.5s ease-in-out;
  transition: all 0.5s ease-in-out;
  -webkit-border-radius: 5px 5px 5px 5px;
  border-radius: 5px 5px 5px 5px;
}

input[type="password"]:focus {
  background-color: #fff;
  border-bottom: 2px solid #3ad135;
}

input[type="password"]:placeholder {
  color: #cccccc;
}

textarea {
  background-color: #f6f6f6;
  border: none;
  color: #0d0d0d;
  padding: 15px 32px;
  text-align: left;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 5px;
  width: 85%;
  font-family: Arial, Helvetica, sans-serif;
  border: 2px solid #f6f6f6;
  -webkit-transition: all 0.5s ease-in-out;
  -moz-transition: all 0.5s ease-in-out;
  -ms-transition: all 0.5s ease-in-out;
  -o-transition: all 0.5s ease-in-out;
  transition: all 0.5s ease-in-out;
  -webkit-border-radius: 5px 5px 5px 5px;
  border-radius: 5px 5px 5px 5px;
}

textarea:focus {
  background-color: #fff;
  border-bottom: 2px solid #3ad135;
}

textarea:placeholder {
  color: #cccccc;
  font-family: "Poppins", sans-serif;
}

/* ANIMATIONS */

/* Simple CSS3 Fade-in-down Animation */
.fadeInDown {
  -webkit-animation-name: fadeInDown;
  animation-name: fadeInDown;
  -webkit-animation-duration: 1s;
  animation-duration: 1s;
  -webkit-animation-fill-mode: both;
  animation-fill-mode: both;
}

@-webkit-keyframes fadeInDown {
  0% {
    opacity: 0;
    -webkit-transform: translate3d(0, -100%, 0);
    transform: translate3d(0, -100%, 0);
  }
  100% {
    opacity: 1;
    -webkit-transform: none;
    transform: none;
  }
}

@keyframes fadeInDown {
  0% {
    opacity: 0;
    -webkit-transform: translate3d(0, -100%, 0);
    transform: translate3d(0, -100%, 0);
  }
  100% {
    opacity: 1;
    -webkit-transform: none;
    transform: none;
  }
}

/* Simple CSS3 Fade-in Animation */
@-webkit-keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
@-moz-keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

.fadeIn.second {
  -webkit-animation-delay: 0.6s;
  -moz-animation-delay: 0.6s;
  animation-delay: 0.6s;
}

.fadeIn.third {
  -webkit-animation-delay: 0.8s;
  -moz-animation-delay: 0.8s;
  animation-delay: 0.8s;
}

.fadeIn.fourth {
  -webkit-animation-delay: 1s;
  -moz-animation-delay: 1s;
  animation-delay: 1s;
}

/* Simple CSS3 Fade-in Animation */
.underlineHover:after {
  display: block;
  left: 0;
  bottom: -10px;
  width: 0;
  height: 2px;
  background-color: #3ad135;
  content: "";
  transition: width 0.2s;
}

.underlineHover:hover {
  color: #0d0d0d;
}

.underlineHover:hover:after {
  width: 100%;
}

/* OTHERS */

*:focus {
  outline: none;
}

#icon {
  width: 60%;
}

* {
  box-sizing: border-box;
}
</style>
