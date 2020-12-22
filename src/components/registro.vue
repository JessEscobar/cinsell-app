<template>
  <div id="contenido-registro">
    <header>
      <h1>Cinsell</h1>
    </header>

    <div id="datos-registro">
      <form v-on:submit.prevent="register_user" id="form-register" action="">
        <h2>DATOS PERSONALES</h2>
        <div>
          <label for="">Nombres y apellidos:</label>
          <input
            class="validar-datos"
            placeholder="Digite sus nombres y apellidos"
            type="text"
            v-model="form.nombre"
            required
          />
        </div>
        <div>
          <label for=""># Identificación:</label>
          <input
            class="validar-datos"
            placeholder="Digite su número de identificación"
            type="number"
            v-model="form.nDocumento"
            required
          />
        </div>
        <div>
          <label for="">Teléfono:</label>
          <input
            class="validar-datos"
            placeholder="Digite su número de teléfono"
            type="number"
            v-model="form.telefono"
            required
          />
        </div>
        <div>
          <label for="">Departamento:</label>

          <input
            class="validar-datos"
            placeholder="Digite su departamento de residencia"
            type="text"
            v-model="form.departamento"
            required
          />
        </div>
        <div>
          <label for="">Ciudad:</label>
          <input
            class="validar-datos"
            placeholder="Digite su ciudad de residencia"
            type="text"
            v-model="form.ciudad"
            required
          />
        </div>
        <div>
          <label for="">Dirección:</label>
          <input
            class="validar-datos"
            placeholder="Digite su dirección"
            type="text"
            v-model="form.direccion"
            required
          />
        </div>
        <div>
          <label for="">Nickname:</label>
          <input
            class="validar-datos"
            placeholder="Digite el nickname deseado"
            type="text"
            v-model="form.username"
            required
          />
        </div>
        <div>
          <label for="">Contraseña:</label>
          <input
            class="validar-datos"
            placeholder="Digite la contraseña deseada"
            type="text"
            v-model="form.password"
            required
          />
        </div>
        <div>
          <label for="">Confirmar contraseña:</label>
          <input
            class="validar-datos"
            placeholder="Digite de nuevo la contraseña deseada"
            type="text"
            v-model="con.vericontraseña"
            required
          />
        </div>
        <input class="submit" type="submit" value="Confirmar registro" />
      </form>
    </div>

    <footer>
      <span>Copyright © 2020 MisionTIC2022 G1M3 - Grupo 10</span>
      <span>Todos los Derechos Reservados</span>
    </footer>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "registro",
  data() {
    return {
      form: {
        "username": "",
        "password": "",
        "nDocumento":"",
        "nombre": "",
        "telefono": "",
        "ciudad": "",
        "departamento": "",
        "direccion": ""        
      },
      con:{
            vericontraseña: "",
      }
    };
  },

  methods: {
    register_user() {
      let user = this.form.username;
      let password = this.form.password
      let vericontraseña = this.con.vericontraseña
      let nDocumento = this.form.nDocumento
      let nombre = this.form.nombre
      let telefono = this.form.telefono
      let ciudad = this.form.ciudad
      let departamento = this.form.departamento
      let direccion = this.form.direccion

      let self = this;

      if (password!=vericontraseña){
          alert("Las contraseñas no coinciden")
      }
      else{ 
          console.log(self)
        axios
        .post("https://cinsell.herokuapp.com/crear", this.form)
        .then(result =>{
            let val = result.data.detail
            if (val===true){
                alert("Usuario Registrado correctamente")
                self.$router.push({name:"login"});
            }
            else{
                alert("El usuario ya se encuentra en la base de datos")
            }

        })
        .catch(error => alert("El Nickname ya existe en la base de datos"))
        
      }
    },
  },
};
</script>

<style>
#contenido-registro {
  width: 100%;
  height: 100vh;
  color: black;
  background-color: white;
}

#datos-registro {
  background-color: rgb(223, 223, 223);
  height: 85vh;
}

#datos-registro h2 {
  font-size: 2rem;
  margin: 0 auto 20px auto;
  text-transform: uppercase;
}

#datos-registro #form-register {
  width: 70%;
  height: 100%;
  margin: auto;
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  align-items: flex-start;
}

#form-register .submit {
  margin: 0;
  width: 50%;
  background-color: #3259fe;
  border: none;
  color: white;
  padding: 20px;
  border-radius: 5px;
  margin: 25px auto;
  text-transform: uppercase;
  cursor: pointer;
  font-size: 1.3rem;
  font-weight: 550;
}

#form-register #submit:hover {
  background-color: #1631aa;
  cursor: pointer;
}

#form-register div {
  display: flex;
  justify-content: space-evenly;
  width: 100%;
}

#form-register label {
  width: 40%;
  font-size: 1.3rem;
  text-align: left;
  padding: 10px;
}

#form-register input {
  width: 60%;
  padding: 10px;
  border: none;
  border-radius: 5px;
  cursor: default;
  background-color: white;
  text-align: center;
  font-size: 1.4rem;
  color: black;
  outline: none;
  -webkit-appearance: none;
}
input[type="number"]::-webkit-inner-spin-button,
input[type="number"]::-webkit-outer-spin-button {
  -webkit-appearance: none;
  margin: auto;
}
</style>
