<template>
  <div class="card bg-warning my-5">
    <div class="card-body">
      <b-form @submit.prevent="" autocomplete="off">
        <b-input-group>
          <b-form-tags
            class="bg-warning border-0 text-dark"
            tag-variant="dark"
            placeholder="Adicione tags"
            v-model="tag.nome"
          ></b-form-tags>
        </b-input-group>
      </b-form>
    </div>
  </div>
</template>

<script>
export default {
  name: "n-tag",
  props: {
    id: [Number, String],
  },
  data() {
    return {
      tag: {
        id: null,
        notaId: null,
        nome: null,
      },
    };
  },
  computed: {
    tagObservada() {
      return JSON.parse(JSON.stringify(this.tag));
    },
  },
  watch: {
    tagObservada: {
      handler(value, oldValue) {
        if (this.compararTags(value, oldValue)) {
          if (!this.esperandoAlteracao) {
            setTimeout(() => {
              this.id ? this.editar() : this.adicionar();
              this.esperandoAlteracao = false;
            }, 3000);
          }
          this.esperandoAlteracao = true;
        }
      },
      deep: true,
    },
  },
  methods: {
    compararTags(novaTag, antigaTag) {
      return JSON.stringify(novaTag) != JSON.stringify(antigaTag);
    },
    async adicionar() {
      const tagSaved = await this.$store.dispatch("tag/add", this.tag);

      this.$router.push(`/tag/edit/${tagSaved.id}`);
    },
    async editar() {
      await this.$store.dispatch("tag/edit", this.tag);

      await this.carregar();
    },
    async carregar() {
      const { data } = await this.$axios.get(`tag/${this.id}`);

      this.tag = data;
    },
  },
  async mounted() {
    if (this.id) {
      await this.carregar();
    }
  },
};
</script>

<style>
.nome {
  font-weight: 600;
}
</style>
