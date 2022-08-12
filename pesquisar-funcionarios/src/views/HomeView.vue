<template>
  <div class="home">
    <ComboFuncionarios msg="Pesquisar Funcionários" />
  </div>
</template>

<script>
// @ is an alias to /src
import ComboFuncionarios from "@/components/ComboFuncionarios.vue";

export default {
  name: "HomeView",
  components: {
    ComboFuncionarios,
  },
};
</script>
