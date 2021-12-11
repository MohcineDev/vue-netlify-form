<template>
  <div>
    <h1>You're Awesome! Thank you for your submission!</h1>
    <router-link class="back" to="/">
    </router-link>
  </div>
</template>

<script>
export default {
  name: "SubmissionSuccess",
};
</script>

<style>
div{
  text-align: center;
}
h1{
  margin-bottom: 3rem;

}
.back {
  position: relative;
  display: inline-block;
  width: 30px;
  height: 20px;
}
.back::after,
.back::before {
  content: "";
  position: absolute;
}
.back::before {
  width: 30px;
  height: 3px;
  background:#000;
  top: 50%; 
  left: -5px;
}
.back::after {
  top: 50%; 
  left: 0;
  width: 10px;
  height: 10px;
  transform: rotate(-45deg) translateY(-50%);
  border: 2px solid;
  border-color: #000 transparent transparent #000;
}
</style>