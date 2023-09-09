<script setup>
const route = useRoute();
const router = useRouter();
const nuxtApp = useNuxtApp();

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
        <form class="login-form" ref="loginForm">
          <div class="input-box">
            <input type="text" id="username" required />
            <label for="username">Username</label>
          </div>
          <div class="input-box">
            <input type="password" id="password" required />
            <label for="password">Password</label>
          </div>
          <div class="check-box">
            <input type="checkbox" id="login-checkbox" />
            <label for="login-checkbox">Remember me</label>
            <span>Forgot password?</span>
          </div>
          <button class="submit-button">
            <span></span>
            <span></span>
            <span></span>
            <span></span>
            Login
          </button>

          <div class="text-center mt-4">
            Don't have account? Click here to
            <span
              class="text-white font-bold cursor-pointer"
              @click="showRegisterForm()"
            >
              register!
            </span>
          </div>
        </form>
        <form class="register-form" ref="registerForm">
          <div class="input-box">
            <input type="text" id="username2" required />
            <label for="username2">Username</label>
          </div>
          <div class="input-box">
            <input type="email" id="email" required />
            <label for="email">Email Id</label>
          </div>
          <div class="input-box">
            <input type="password" id="password2" required />
            <label for="password2">Password</label>
          </div>
          <div class="check-box">
            <input type="checkbox" id="register-checkbox" />
            <label for="register-checkbox"
              >Agree to the terms & conditions</label
            >
          </div>
          <button class="submit-button">
            <span></span>
            <span></span>
            <span></span>
            <span></span>
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
        </form>
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
