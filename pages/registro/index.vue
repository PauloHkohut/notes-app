<template>
  <div>
    <h1 class="my-5">Novo usuário</h1>
    
    <b-card class="p-4">
      <div class="row">
        <div class="col-md-9">
          <b-form @submit.prevent="salvar">
            <b-form-group label-align="left" label-cols="1" label="Nome">
              <b-form-input
                name="nome"
                v-model="usuario.nome"
                type="text"
                id="nome"
                autocomplete="off"
                required
              ></b-form-input>
            </b-form-group>

            <b-form-group label-align="left" label-cols="1" label="E-mail">
              <b-form-input
                name="email"
                v-model="usuario.email"
                type="email"
                id="email"
                autocomplete="off"
                required
              ></b-form-input>
            </b-form-group>

            <b-form-group label-align="left" label-cols="1" label="Senha">
              <b-form-input
                name="senha"
                v-model="usuario.senha"
                type="password"
                id="senha"
                required
              ></b-form-input>
            </b-form-group>

            <div class="row">
              <div class="col-md-10 offset-md-2">
                <b-button type="submit" variant="primary"
                  >Salvar usuário</b-button
                >
              </div>
            </div>
          </b-form>
        </div>
      </div>
    </b-card>
  </div>
</template>

<script>
export default {
  layout: "home",
  data() {
    return {
      usuario: {
        nome: '',
        email: '',
        senha: ''
      }
    };
  },
  methods: {
    async salvar() {
      try {
        let data = {
          nome: this.usuario.nome,
          email: this.usuario.email,
          senha: this.usuario.senha
        };

        await this.$axios.post(`usuario`, data);

        window.alert('Usuário registrado com sucesso!');

        this.$router.push("../login");
      } catch (e) {
        window.alert('Não foi possível registrar o usuário!');
        console.log(e);
      }
    }
  },
};
</script>

<style></style>
