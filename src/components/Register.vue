<template>
  <div>
    <div class="container mt-5">
    <h3>Registro</h3>
    <form v-on:submit.prevent="register">
      <div class="form-group">
        <label>Nombre</label>
        <input type="text" class="form-control" placeholder="Nombre" v-model="name">
      </div>
      <div class="form-group">
        <label>Apellidos</label>
        <input type="text" class="form-control" placeholder="Apellidos" v-model="lastname">
      </div>
      <div class="form-group">
        <label>Número de colegiado</label>
        <input type="text" class="form-control" placeholder="Introduce tu número de colegiado" v-model="numICA">
      </div>
      <div class="form-group">
        <label for="exampleInputEmail1">Email</label>
        <input type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" placeholder="Introduce tu email" v-model="email">
      </div>
      <div class="form-group">
        <label for="exampleInputPassword1">Contraseña</label>
        <input type="password" class="form-control" id="exampleInputPassword1" placeholder="Contraseña" v-model="pass">
      </div>
      <div class="form-group">
        <label for="exampleInputPassword1">Confirma contraseña</label>
        <input type="password" class="form-control" id="exampleInputPassword2" placeholder="Confirma contraseña" v-model="confirmpass">
      </div>
      <button type="submit" class="btn btn-primary">Registrarte</button>
    </form>
    </div>
  </div>
</template>

<script>
import {auth} from '../firebase'
import { db } from "../firebase";

export default {
  data() {
    return{
      name: "",
      lastname:"",
      numICA: "",
      email:"",
      pass:"",
      confirmpass: ""
    }
  },
  created: function () {
    //console.log(auth.currentUser.uid)
  },
  methods:{
    register(){
      auth.createUserWithEmailAndPassword(this.email, this.pass).then( 
        (user) => {
          var uid = auth.currentUser.uid;
          db.ref("lawyers").child(uid).set({email: this.email, name: this.name, lastname: this.lastname, numICA: this.numICA});


          // this.$router.replace('perfilabogado')
          this.$router.replace("/perfilabogado")
        },
      function(err) {
          alert(err)
      });   
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>

</style>
