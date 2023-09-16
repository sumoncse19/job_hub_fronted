<script setup>
const route = useRoute();
const router = useRouter();
const nuxtApp = useNuxtApp();
import { useUserStore } from "~/stores/user";

const userStore = useUserStore();

// For form data:
const emailLogin = ref("");
const passwordLogin = ref("");
const isRememberMe = ref(false);

const fullNameRegister = ref("");
const emailRegister = ref("");
const passwordRegister = ref("");
const confirmPasswordRegister = ref("");
const isAgree = ref(false);

const btnActiveBack = ref(null);
const loginForm = ref(null);
const registerForm = ref(null);

const showLoginForm = () => {
  if (btnActiveBack.value && registerForm.value && loginForm.value) {
    btnActiveBack.value.style.left = "0px";
    registerForm.value.style.left = "115%";
    loginForm.value.style.left = "0px";
    setTimeout(() => {
      router.push("/auth/login");
    }, 500);
  }
};

const showRegisterForm = () => {
  if (btnActiveBack.value && registerForm.value && loginForm.value) {
    btnActiveBack.value.style.left = "50%";
    registerForm.value.style.left = "0px";
    loginForm.value.style.left = "-115%";
    setTimeout(() => {
      router.push("/auth/register");
    }, 500);
  }
};

const loginButton = ref(null);
const registerButton = ref(null);

const setupEventListeners = () => {
  if (loginButton.value && registerButton.value) {
    loginButton.value.addEventListener("click", () => {
      showLoginForm();
    });

    registerButton.value.addEventListener("click", () => {
      showRegisterForm();
    });
  }
};

onMounted(() => {
  if (route.fullPath.includes("register")) {
    showRegisterForm();
  } else if (route.fullPath.includes("login")) {
    showLoginForm();
  } else {
    router.push("/");
  }
  setupEventListeners();
});

// methods
const handleLogin = async () => {
  await $fetch(`http://127.0.0.1:8000/api/v1/token/login`, {
    method: "POST",
    body: {
      username: emailLogin.value,
      password: passwordLogin.value,
    },
  })
    .then((data) => {
      console.log(data.auth_token, "here the response of login");
      userStore.setToken(data.auth_token, emailLogin.value);
      router.push({ path: "/" });
    })
    .catch((error) => {
      if (error.response) {
        for (const property in error.response._data) {
          error.value.push(`${property}: ${error.response._data[property]}`);
        }
        console.log(JSON.stringify(error.response));
      } else if (error.message) {
        error.value.push("Something went wrong. Please try again.");
        console.log(JSON.stringify(error));
      }
    });
  console.log(
    "from handleLogin",
    emailLogin.value,
    passwordLogin.value,
    isRememberMe.value
  );
};
const handleRegister = async () => {
  await $fetch(`http://127.0.0.1:8000/api/v1/users/`, {
    method: "POST",
    body: {
      // name: fullNameRegister.value,
      // password: passwordRegister.value,
      // isAgree: isAgree.value,
      firstname: fullNameRegister.value,
      username: fullNameRegister.value,
      email: emailRegister.value,
      password: passwordRegister.value,
    },
  })
    .then((response) => {
      console.log(response, "here the response of registration");
      router.push("/auth/login");
    })
    .catch((error) => {
      if (error.response) {
        for (const property in error.response._data) {
          error.value.push(`${property}: ${error.response._data[property]}`);
        }
        console.log(JSON.stringify(error.response));
      } else if (error.message) {
        error.value.push("Something went wrong. Please try again.");
        console.log(JSON.stringify(error));
      }
    });
  console.log(
    "from handleRegister",
    fullNameRegister.value,
    emailRegister.value,
    passwordRegister.value,
    confirmPasswordRegister.value,
    isAgree.value
  );
};
</script>

<template>
  <div class="w-full flex justify-center">
    <div class="mainDiv">
      <div class="button-box">
        <div class="btn-active-back" ref="btnActiveBack"></div>
        <button class="toggle-btn login-btn" @click="showLoginForm">
          &nbsp;&nbsp;Login
        </button>
        <button class="toggle-btn register-btn" @click="showRegisterForm">
          &nbsp;&nbsp;Register
        </button>
      </div>
      <div class="form-box">
        <div class="login-form formDiv" ref="loginForm">
          <div class="input-box">
            <input v-model="emailLogin" type="email" id="emailLogin" required />
            <label for="emailLogin">Email Id</label>
          </div>
          <div class="input-box">
            <input
              v-model="passwordLogin"
              type="passwordLogin"
              id="passwordLogin"
              required
            />
            <label for="passwordLogin">Password</label>
          </div>
          <div class="check-box">
            <input v-model="isRememberMe" type="checkbox" id="login-checkbox" />
            <label for="login-checkbox">Remember me</label>
            <span>Forgot password?</span>
          </div>
          <button class="submit-button" @click="handleLogin">Login</button>

          <div class="text-center mt-4">
            Don't have account? Click here to
            <span
              class="text-white font-bold cursor-pointer"
              @click="showRegisterForm()"
            >
              register!
            </span>
          </div>
        </div>
        <div class="register-form formDiv" ref="registerForm">
          <div class="input-box">
            <input
              v-model="fullNameRegister"
              type="text"
              id="fullNameRegister"
              required
            />
            <label for="fullNameRegister">Full Name</label>
          </div>
          <div class="input-box">
            <input
              v-model="emailRegister"
              type="email"
              id="emailRegister"
              required
            />
            <label for="emailRegister">Email Id</label>
          </div>
          <div class="input-box">
            <input
              v-model="passwordRegister"
              type="password"
              id="passwordRegister"
              required
            />
            <label for="passwordRegister">Password</label>
          </div>
          <div class="input-box">
            <input
              v-model="confirmPasswordRegister"
              type="password"
              id="confirmPasswordRegister"
              required
            />
            <label for="confirmPasswordRegister">Confirm Password</label>
          </div>
          <div class="check-box">
            <input v-model="isAgree" type="checkbox" id="register-checkbox" />
            <label for="register-checkbox"
              >Agree to the terms & conditions</label
            >
          </div>
          <button class="submit-button" @click="handleRegister">
            Register
          </button>

          <div class="text-center mt-2">
            Already registered? Click here to
            <span
              @click="showLoginForm()"
              class="text-white font-bold cursor-pointer"
            >
              login!
            </span>
          </div>
        </div>
      </div>

      <div class="other-options">
        <div class="another-option">or</div>
        <div class="social-icons">
          <BaseIconFacebook fill="white" />
          <BaseIconApple fill="white" />
          <BaseIconGoogle fill="white" />
          <BaseIconTwitter fill="white" />
          <BaseIconInstagram fill="white" />
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
@import "~/assets/scss/auth.scss";
</style>
