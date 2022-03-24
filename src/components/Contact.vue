<template>
  <section class="contact">
    <h2>Contact Us</h2>
    <form
      name="contactus"
      method="POST"
      @submit.prevent="checkforErrors"
      data-netlify="true"
    >
      <input type="hidden" name="form-name" value="contactus" />
      <div>
        <label>Full Name</label>
        <input
          type="text"
          required
          name="fullname"
          v-model="form.fullname"
          placeholder="Full Name"
          id="fullname"
        />
        <span v-if="errors.fullnameError" v-text="errors.fullnameError"></span>
      </div>
      <div>
        <label>Email</label>

        <input
          type="email"
          required
          name="email"
          v-model="form.email"
          placeholder="email"
        />
        <span v-if="errors.emailError" v-text="errors.emailError"></span>
      </div>
      <div>
        <label>Phone Number</label>
        <input
          type="tel"
          name="tel"
          v-model="form.tel"
          placeholder="Phone Number"
        />
        <span v-if="errors.telError" v-text="errors.telError"></span>
      </div>
      <div>
        <label>Your Message</label>
        <textarea
          name="msg"
          cols="30"
          required
          rows="5"
          maxlength="100"
          v-model="form.msg"
          placeholder="Your Message..."
        ></textarea>
        <span v-if="errors.msgError" v-text="errors.msgError"></span>
      </div>
      <input type="submit" value="Submit" />
    </form>
  </section>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      errors: {
        fullnameError: "",
        emailError: "",
        telError: "",
        msgError: "",
      },
      form: {
        fullname: "",
        email: "",
        tel: "",
        msg: "",
      },
    };
  },

  methods: {
    checkforErrors() {
      if (this.form.fullname.trim() == "") {
        this.errors.fullnameError = "enter your full name";
      } else if (this.form.fullname.trim().length < 6) {
        this.errors.fullnameError = "please enter a valid full name";
      } else if (this.form.email.trim() == "") {
        this.errors.emailError = "enter your email";
      } else if (this.form.email.trim().length < 6) {
        this.errors.fullnameError = "";
        this.errors.emailError = "please enter a valid email";
      } else if (this.form.msg.trim() == "") {
        this.errors.emailError = "";
        this.errors.msgError = "please enter your msg here";
      } else {
        this.handleSubmit();
      }
    },
    encode(data) {
      return Object.keys(data)
        .map(
          (key) => `${encodeURIComponent(key)}=${encodeURIComponent(data[key])}`
        )
        .join("&");
    },
    handleSubmit() {
      // const axiosConfig = {
      //   header: { "Content-Type": "application/x-www-form-urlencoded" },
      // };
      fetch("/", {
        method: "POST",
        headers: { "Content-Type": "application/x-www-form-urlencoded" },
        "form-name": "contactus",
        body: this.encode({
          ...this.form,
        }),
      })
        .then(() => {
          this.$router.push("thanks");
        })
        .catch(() => {
          this.$router.push("404");
        });

      //  axios.post(
      //   "/",
      //   this.encode({
      //     "form-name": "contactus",
      //     ...this.form,
      //   }),
      //   axiosConfig
      // )
    },
  },
};
</script>

<style scoped>
section {
  max-width: 1200px;
  margin: auto;
}
h2 {
  color: #42b983;
}
form {
  width: 50%;
  margin: auto;
}
form div {
  position: relative;
  padding-bottom: 1rem;
}
form div span {
  position: absolute;
  left: 10px;
  bottom: 0;
  font-size: 14px;
  color: rgb(181, 82, 100);
}
label {
  display: block;
  margin-top: 5px;
  color: #4d148c;
  text-align: left;
}

input,
textarea {
  width: 100%;
  outline: none;
  border: 1px solid #ddd;
  color: #4d148c;
  padding: 10px;
  border-radius: 8px;
  margin: auto;
  box-sizing: border-box;
  font-size: 1rem;
}
textarea {
  resize: none;
}

input[type="submit"] {
  display: block;
  color: #4d148c;
  padding: 8px 1rem;
  font-weight: 800;
  font-size: 1rem;
  width: 200px;
  margin: 1rem auto;
  border: 2px solid #fff;
  cursor: pointer;
}

/* Medium devices */
@media only screen and (max-width: 768px) {
  form {
    width: 80%;
  }
}
</style>