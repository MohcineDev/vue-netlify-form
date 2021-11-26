<template>
  <section class="contact">
    <h2>contact us</h2>
    <form name="contactus" method="POST" @submit.prevent="handleSubmit" data-netlify="true">
      <input type="hidden" name="form-name" value="contactus" />
      <label>Full Name</label>
      <input
        type="text"
        required
        name="fullname"
        v-model="form.fullname"
        placeholder="Full Name"
        id="fullname"
        minlength="4"
      />
      <label>Email</label>
      <input
        type="email"
        required
        name="email"
        v-model="form.email"
        placeholder="email"
        minlength="8"
      />
      <label>Phone Number</label>
      <input
        type="tel"
        required
        name="tel"
        v-model="form.tel"
        placeholder="Phone Number"
        minlength="9"
      />
      <label>Your Message</label>
      <textarea
        name="msg"
        cols="30"
        required
        rows="5"
        minlength="10"
        maxlength="100"
        v-model="form.msg"
        placeholder="Your Message..."
      ></textarea>
      <button type="submit">Send</button>
      <!-- <input type="submit" value="Submit" /> -->
    </form>
  </section>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      form: {
        fullname: "",
        email: "",
        tel: "",
        msg: "",
      },
    };
  },

  methods: {
    encode(data) {
      return Object.keys(data)
        .map(
          (key) => `${encodeURIComponent(key)}=${encodeURIComponent(data[key])}`
        )
        .join("&");
    },
    handleSubmit() {
      console.log(123);
      // const axiosConfig = {
      //   header: { "Content-Type": "application/x-www-form-urlencoded" },
      // }; 
        fetch("/", {
        method: "POST",
        headers: { "Content-Type": "application/x-www-form-urlencoded" },
        body: this.encode({
          "form-name": "contactus",
          ...this.form,
        }),
      }).then(() => {
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
  color: #ff6200;
}
form {
  width: 50%;
  margin: auto;
}
label {
  display: block;
  margin-top: 1rem;
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