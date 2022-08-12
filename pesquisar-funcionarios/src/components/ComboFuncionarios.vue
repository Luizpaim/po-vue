<template>
  <div class="hello">
    <h1>{{ msg }}</h1>

    <div class="paramsSexo">
      <label> Sexo </label>
      <select name="sexo" id="sexo" v-model="this.paramsSexo">
        <option value="Masculino">Masculino</option>
        <option value="Feminino">Feminino</option></select
      ><br />

      <template v-if="this.paramsSexo">
        <label> Funcionario </label>
        <select name="funcionario" id="funcionario" v-model="this.paramsNome">
          <option
            v-for="(dados, index) in this.filtrarDadosParams()"
            :key="index"
            :value="dados.nome"
          >
            {{ dados.nome }}
          </option>
        </select>
      </template>
    </div>

    <template v-if="this.filtrarDadosNome()"
      ><div class="tabelaFuncionarios">
        <table v-for="(dados, index) in this.filtrarDadosNome()" :key="index">
          <thead>
            <tr>
              <th>Nome</th>
              <th>Idade</th>
              <th>CPF</th>
              <th>Data nascimento</th>
              <th>Sexo</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td>{{ dados.nome }}</td>
              <td>{{ dados.idade }}</td>
              <td>{{ dados.cpf }}</td>
              <td>{{ dados.data_nasc }}</td>
              <td>{{ dados.sexo }}</td>
            </tr>
          </tbody>
        </table>
      </div></template
    >
  </div>
</template>

<script>
export default {
  name: "ComboFuncionarios",
  props: {
    msg: String,
  },

  data() {
    return {
      dadosFuncionarios: [],
      dadosParams: undefined,
      dadosNome: undefined,
      paramsSexo: undefined,
      paramsNome: undefined,
    };
  },
  methods: {
    pegarDadosApi() {
      this.axios
        .get("https://run.mocky.io/v3/d480880b-059e-47cf-9ca7-b38d805f1d40")
        .then((response) => {
          this.dadosFuncionarios = response.data;
          // console.log(this.dadosFuncionarios);
        });
    },
    filtrarDadosParams() {
      this.dadosParams = this.dadosFuncionarios.filter(
        (dados) => dados.sexo == this.paramsSexo
      );
      return this.dadosParams;
    },
    filtrarDadosNome() {
      this.dadosNome = this.dadosFuncionarios.filter(
        (dados) => dados.nome == this.paramsNome
      );
      console.log(this.paramsNome);

      console.log(this.dadosNome);
      return this.dadosNome;
    },
  },

  created() {
    this.pegarDadosApi();
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
