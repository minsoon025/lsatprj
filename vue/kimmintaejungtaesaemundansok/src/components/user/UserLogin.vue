<template>
  <section class="py-5">
    <div class="container px-5">
      <!-- Contact form-->
      <div class="bg-light rounded-4 py-5 px-4 px-md-5">
        <div class="text-center mb-5">
          <div
            class="feature bg-primary bg-gradient-primary-to-secondary text-white rounded-3 mb-3"
          >
            <a href="regist.html" target="_blank">
              <i class="bi bi-person-add"></i>
            </a>
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="30"
              height="30"
              fill="currentColor"
              class="bi bi-person-add"
              viewBox="0 0 16 16"
            >
              <path
                d="M12.5 16a3.5 3.5 0 1 0 0-7 3.5 3.5 0 0 0 0 7Zm.5-5v1h1a.5.5 0 0 1 0 1h-1v1a.5.5 0 0 1-1 0v-1h-1a.5.5 0 0 1 0-1h1v-1a.5.5 0 0 1 1 0Zm-2-6a3 3 0 1 1-6 0 3 3 0 0 1 6 0ZM8 7a2 2 0 1 0 0-4 2 2 0 0 0 0 4Z"
              />
              <path
                d="M8.256 14a4.474 4.474 0 0 1-.229-1.004H3c.001-.246.154-.986.832-1.664C4.484 10.68 5.711 10 8 10c.26 0 .507.009.74.025.226-.341.496-.65.804-.918C9.077 9.038 8.564 9 8 9c-5 0-6 3-6 4s1 1 1 1h5.256Z"
              />
            </svg>
          </div>
          <h1 class="fw-bolder">로그인</h1>
          <p class="lead fw-normal text-muted mb-0">
            Let's together!
            <br />
          </p>
        </div>
        <div class="row gx-5 justify-content-center">
          <div class="col-lg-8 col-xl-6">
            <form id="contactForm" data-sb-form-api-token="API_TOKEN">
              <!-- id input-->
              <div class="form-floating mb-3">
                <input
                  v-model="id"
                  class="form-control"
                  id="id"
                  type="text"
                  placeholder=" "
                  data-sb-validations="required"
                />
                <label for="id">아이디</label>
                <!-- 이거 얻다 쓰는 거야??? 아마 아이디 입력 안하면 뜨는 건것 같은데 -->
                <div class="invalid-feedback" data-sb-feedback="id:required">
                  아이디를 입력해주세요.
                </div>
              </div>

              <!-- pw input-->
              <div class="form-floating mb-3">
                <input
                  v-model="password"
                  class="form-control"
                  id="password"
                  type="password"
                  placeholder=" "
                  data-sb-validations="required,email"
                />
                <label for="password">비밀번호</label>
                <div
                  class="invalid-feedback"
                  data-sb-feedback="password:required"
                >
                  비밀번호를 입력해주세요.
                </div>
                <!-- <div
                      class="invalid-feedback"
                      data-sb-feedback="email:email"
                    ></div> -->
              </div>
              <div class="d-none" id="submitSuccessMessage">
                <div class="text-center mb-3">
                  <div class="fw-bolder">Form submission successful!</div>
                  To activate this form, sign up at
                  <br />
                  <a href="https://startbootstrap.com/solution/contact-forms"
                    >https://startbootstrap.com/solution/contact-forms</a
                  >
                </div>
              </div>

              <div class="d-none" id="submitErrorMessage"></div>
              <!-- Submit Button-->
              <div class="idflex">
                <a
                  class="btn btn-primary btn-lg px-5 py-3 me-sm-3 fs-6 fw-bolder"
                  @click="login"
                  >로그인</a
                >
                <a
                  class="btn btn-primary btn-lg px-5 py-3 me-sm-3 fs-6 fw-bolder"
                  href="/user/regist"
                  >회원가입</a
                >
              </div>
            </form>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
<script>
import http from "../../util/http-common";

export default {
  data() {
    return {
      id: "",
      password: "",
    };
  },
  methods: {
    login() {
      console.log("로그인 기능!");
      // http.get("/video")
      // .then((res) => {
      //   console.log(res.data)
      // })
      http({
        url: "/user/login",
        method: "GET",
        params: {
          id: this.id,
          level: 0,
          name: "",
          password: this.password,
        },
      }).then((res) => {
        console.log(res.data);
        if (typeof res.data == "object") {
          sessionStorage.setItem("user", this.id);
          console.log("로그인 완료");
          this.$router.push({ name: "user-info" });
          // this.$router.push({ path: "/", query: {id: this.id} })
        } else {
          console.log("로그인 실패");
          alert(res.data);
        }
      });
    },
  },
  created() {
    if (sessionStorage.getItem("user") != null) {
      console.log(">> 로그인 된 상태");
      this.$router.push({ name: "user-info" });
    } else {
      console.log(">> 로그인 안된 상태");
    }
  },
};
</script>

<style></style>
