
<template>
  <dir class="contain-fluid">
    <div class="row mt-3">
      <div class="col-xs-12 col-sm-7 col-md-12 col-lg-12 col-xl-12">
        <div class="login-form">
          <h2 class="login-heading">Login</h2>
          <b-form @submit.prevent="login">
            <div class="col-sm-12">
              <b-form-group label="Email:" label-for="email">
                <b-input
                  type="email"
                  name="email"
                  placeholder="Ingrese su Email"
                  id="email"
                  class="login-input"
                  v-model="form.email"
                />
              </b-form-group>
            </div>

            <div class="col-sm-12">
              <!-- <label for="password">Password</label> -->
              <b-form-group label="Contraseña:" label-for="password">
                <b-input
                  placeholder="Ingrese su contraseña"
                  type="password"
                  name="password"
                  id="password"
                  class="login-input"
                  v-model="form.password"
                />
              </b-form-group>
            </div>

            <div class="col-xs-12 offset-sm-5">
              <br>
              <button type="submit" class="btn btn-dark" :disabled="guardando">Registrar</button>
            </div>
          </b-form>
        </div>
      </div>
    </div>
  </dir>
</template>

<script>
import { db } from "../services/firebase";

export default {
  data() {
    return {
      form: {
        email: "",
        password: ""
      },
      guardando: false
    };
  },
  methods: {
    login() {
      db.collection("personas")
        .add(this.form)
        .then(response => {
          this.$router.push({ path: "/productos" });
          alert("El usuario a sido registrado");
        });
    }
  }
};
</script>