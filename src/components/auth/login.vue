<template>
 <div class="container" style="width:600px;background-color:#92D9E9;">
 <div class="row">
 <div class="col-lg-6 offset-lg-3 col-sm-10 offset-sm-1">
 <form
 class="text-center"
 style="margin-top:70px;height:auto;"
 @submit.prevent="loginUser"
 >
 <h1 class="h3 mb-3 font-weight-normal" style="textalign: center"> Inicio de sesión</h1>
 <input
 type="text"
 id="user"
 class="form-control mb-5"
 placeholder="Usuario"
 v-model="login.user"
 />
 <input
 type="email"
 id="email"
 class="form-control mb-5"
 placeholder="Email"
 v-model="login.email"
 />
 
 <input
 type="password"
 id="password"
 class="form-control mb-5"
 placeholder="Contraseña"
 v-model="login.password"
 />
 
 <center>
 <button class="btn btn-light btn-block w-75 my4 mb-5" type="submit">
 Iniciar sesión
 </button>
 </center>
 </form>
 </div>
 </div>
 </div>
</template>
<script>
import swal from "sweetalert";
export default {
 data() {
 return {
 login: {
     user:"",
 email: "",
 password: ""
 }
 };
 },
 methods: {
 async loginUser() {
 try {
 let response = await this.$http.post("/api/auth/signin", this.login)
;
 console.log(response.data);
 let token = response.data.accessToken;
 localStorage.setItem("jwt", token);
 if (token) {
 swal("Exitoso", "El acceso fue exitoso", "success");
 this.$router.push("/home");
 }
 } catch (err) {
 swal("Error", "Datos inválidos", "error");
 console.log(err.response);
 }
 }
 }
};
</script>