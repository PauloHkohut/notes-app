<template>
  <div>
    <ul class="list-unstyled">
      <li v-for="(item, index) of value" :key="index">
        <n-taglist-item v-model="value[index]"></n-taglist-item>
      </li>
      <li>
        <n-taglist-item
          v-model="tag"
          @itemConfirmado="adicionar()"
        ></n-taglist-item>
      </li>
    </ul>

    <p class="text-muted">
      <small>{{ mensagemNumeroItens }} </small>
    </p>
  </div>
</template>

<script>
export default {
  name: "n-taglist",
  props: {
    value: Array
  },
  data() {
    return {
      tag: {
        nome: null
      }
    };
  },
  computed: {
    numeroItens() {
      return this.value.length;
    },
    mensagemNumeroItens() {
      return this.value.length > 1
        ? `${this.numeroItens} itens adicionados`
        : `${this.numeroItens} item adicionado`;
    }
  },
  methods: {
    adicionar() {
      this.value.push(this.tag);

      this.tag = {
        nome: null
      };
    }
  }
};
</script>

<style></style>
