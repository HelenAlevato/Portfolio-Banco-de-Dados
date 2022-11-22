## Meu Quarto API  📚

#### Em 2022-1 (API 4)
Trabalhei no projeto da API do quarto semestre como desenvolvedora front-end. Com a empresa Oracle como parceira. [GitLab do projeto.](https://gitlab.com/vueforce1/lefoot)<br> 
- **Nome do Grupo:** VueForce
- **Nome do Software:**  LeFoot
- **Visão do Produto:** Ajudar na tomada de decisões de gerentes e diretores com relação a tomada de decisão para campanhas e compras de determinados produtos.
- **Vídeo final de apresentação do [Sistema LeFoot](https://www.youtube.com/watch?v=f8h0w4pPKz4&t=1s)**
     
 - **Objetivo do Produto:** 
	 - Segmentar a venda de produtos nas regiões de São José dos Campos para descobrir novas demandas de produtos por regiões, melhorando a visibilidade da base de clientes a partir da leitura de arquivos *.CSV. A aplicação poderá auxiliar na tomada de decisões dos gerentes e diretores com relação a campanhas e compras de determinados produtos.
  
- **Problema (Desafio):** 

	- O desafio era criar um sistema que mostrasse indices coerentes para toamada de decisão de gestores e diretores de lojas de sapatos.

- **Proposta:**

	- Tela de Cadastro: Para o usuário fazer seu cadastro;
	- E-mail desparado quando o cadastro for feito;
	- Tela de Login: Para o usuário logar no sistema;
	- Tela de Upload de CSV: Baixa as informações do CSV e grava no banco de dados;
	- Tela de Filtrar Clientes: Filtra os clientes por: Gênero, Região, Categoria do sapato e Cor;
	- Tela de Dashboard: Mostrar as análises por meio de 3 graficos que seriam:
		- Gráfico de barras da soma de todos os produtos por gênero
		- Gráfico de donut dos produtos mais vendidos por gênero
		- Gráfico de linhas do valor gasto por gênero para cada região

#### Tecnologias Utilizadas 🛠
- Vue
- JavaScript
- Oracle
- Java
- Git
- GitLab

## Contribuições Pessoais 👩
Nesse trabalho fiquei como Team Dev, responsavel pela parte de front-end. 
Referente a parte de planejamento fiz os desenhos da tela pelo figma e o modo de navegação, como ficaria no projeto final.
Na parte de back-end contribui apenas com uma correção de organização referente aos dados exibidos na Tela de Filtrar Clientes.
No front-end onde tive mais atuação fiz as telas e ligações com o back-end, as atividades dividi em alguns tópicos abaixo:

**Desenvolvimento:**  

<details>
  <summary>Desenvolvimento das telas Redefinição de Senha (front-end)</summary>
  
  ```javascript
  <template>
  <div id="painelRedefinir">
      <h3 style="font-size: 30px;">Redefinir Senha</h3> 

      <span style="margin: 1rem; display: flex; flex-direction: column">
        <label for="nome1">Nome </label>
        <input type="text" />
      </span> 
      <span style="margin: 1rem; display: flex; flex-direction: column">
        <label for="email1">Email </label>
        <input type="text" />
      </span> 
      <span style="margin: 1rem; display: flex; flex-direction: column">
        <label for="novaSenha">Nova Senha </label>
        <input type="password" />
      </span> 
      <span style="margin: 1rem; display: flex; flex-direction: column">
        <label for="confirmeSenha">Confirme a senha </label>
        <input type="password" />
      </span> 

      <Button style="margin-top: 10px">Redefinir</Button>
  </div>
</template>
  ```
</details>

<details>
  <summary>Tela de Upload CSV</summary>
  
  ```javascript
  <template>
  <div id="card">
      <h3 style="font-size: 30px; text-align: center">Carregar arquivo CSV</h3> 

    <form>
        <div style="display: flex; justify-content: center;">
            <label for="arquivo">Insira arquivo aqui</label>
            <input type="file" name="arquivo" id="arquivo" accept=".csv">
        </div>
    </form>
      <div style="display: grid; grid-template-columns: 1fr 1fr; grid-column-gap: 32px;">
        <Button style="margin-top: 10px">Voltar</Button>
        <Button style="margin-top: 10px">Carregar</Button>

      </div>
  </div>
</template>
  ```
</details>

<details>
  <summary>Desenvolvimento tela Login (front-end)</summary>
  
  ```javascript
  <template>
  <div id="painelRedefinir">
    <h3 style="font-size: 30px">LeFoot</h3>

    <span style="margin: 1rem; display: flex; flex-direction: column">
      <label for="nome1"> Nome </label>
      <input type="text" ref="userName"/>
    </span>
    <span style="margin: 1rem; display: flex; flex-direction: column">
      <label for="senha"> Senha </label>
      <input type="password" ref="password"/>
    </span>

    <Button class="button is-dark is-small" style="margin-top: 10px" @click="login">Entrar</Button>
    
  </div>
</template>

<script>
import axios from 'axios';
  
  export default {
    // data: () => (),
    methods: {
      login() {
        const username = this.$refs.userName.value;
        const password = this.$refs.password.value;

        const headers = { 'Content-Type': 'application/json'}

        const body = { username, password }

        axios.post('http://localhost:8081/api/auth/signin', body, headers)
        .then(result => {
          const token = result.data.accessToken;
          localStorage.setItem('userToken', token);
          
          this.$router.push('/')

        })
      }
    }
    
  }
  ```
</details>

<details>
  <summary>Desenvolvimento Tela Criar Conta (front-end)</summary>
  
  ```javascript
	<template>
  <div id="painelRedefinir">
    <h3 style="font-size: 30px">Criar Conta</h3>

    <span style="margin: 1rem; display: flex; flex-direction: column">
      <label for="nome1">Nome do usuário </label>
      <input type="text" ref="userName" maxlength="20" minlength="5" />
    </span>

    <span style="margin: 1rem; display: flex; flex-direction: column">
      <label for="senha"> Nome </label>
      <input type="text" ref="firstName" />
    </span>

    <span style="margin: 1rem; display: flex; flex-direction: column">
      <label for="senha"> Sobrenome </label>
      <input type="text" ref="lastName" />
    </span>

    <span style="margin: 1rem; display: flex; flex-direction: column">
      <label for="email1">E-mail </label>
      <input type="text" ref="email" />
    </span>

    <span style="margin: 1rem; display: flex; flex-direction: column">
      <label for="senha"> Senha </label>
      <input type="password" ref="password" />
    </span>

    <Button
      class="button is-dark is-smal"
      style="margin-top: 10px"
      :disabled="isLoading"
      @click="
        () => {
          this.isLoading = true;
          signup();
        }
      "
      >Criar</Button
    >

    <span v-if="mensagem">{{ mensagem }}</span>
    <ol class="lista-erros has-text-danger">
      <li v-for="erro in this.erros" :key="erro.msg">
        <span style="font-weight: bold">{{erro.campo}}</span>: {{erro.msg}}
      </li>
    </ol>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      mensagem: "",
      erroSenha: false,
      isLoading: false,
      erros: [],
    };
  },

  methods: {
    signup() {
      const username = this.$refs.userName.value;
      const firstName = this.$refs.firstName.value;
      const lastName = this.$refs.lastName.value;
      const email = this.$refs.email.value;
      const password = this.$refs.password.value;

      const headers = { "Content-Type": "application/json" };

      const body = {
        username,
        password,
        email,
        fname: firstName,
        lname: lastName,
        status: "ativo",
        role: ["ROLE_USER"],
      };

      axios
        .post("http://localhost:8081/api/auth/signup", body, headers)
        .then((result) => {
          console.log("teste teste");
          if (result.status === 200) {
            this.mensagem = `Usuário ${username} criado com sucesso, acesse a tela de login para acessar a aplicação!`;
          }
        })
        .catch((error) => {
          const allErrors = error.response.data.errors;
          if (allErrors) {
            this.erros = allErrors.map((erro) => ({
              campo: erro.field,
              msg: erro.defaultMessage,
            }));
          } else {
            alert(error);
          }
        })
        .finally(() => {
          this.isLoading = false;
        });
    },
  },
};
</script>

<style scoped>
.inputError {
  color: red;
}

#painelRedefinir {
  width: 30%;
  min-width: 20%;
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  flex-direction: column;
  /* color: white; */
  background-color: white;
  padding: 20px;
  border-radius: 10px;
  border: 1px solid rgb(148, 148, 148);
  box-shadow: 1px 2px 2px rgba(0, 0, 0, 0.733);
}
label {
  font-weight: 700;
  letter-spacing: 0.5px;
  font-size: 1rem;
  color: rgb(59, 59, 59);
}
button {
  padding: 5px;
  border: none;
}
input {
  padding: 5px;
}
#app {
}
.app-container {
  background-color: white;
  text-align: center;
}
body #app .p-button {
  margin-left: 0.2em;
}
form {
  margin-top: 2em;
}
.lista-erros {
  padding: 10px;
  display: flex;
  justify-content: center;
}
</style>

  ```
</details>

<details>
  <summary>Paginação da tela Filtrar clientes</summary>
  
  ```javascript
    <!-- Barra de paginação -->
    <div v-if="listaFiltrada.length > 0" class="table-container">
      <div style="width: 50%">
        <nav
          class="pagination is-right"
          role="navigation"
          aria-label="pagination"
        >
          <label>{{ paginaAtual + 1 }}</label>
          <a class="pagination-previous" style="color: white" @click="paginaAnterior">Previous</a>
          <a class="pagination-next" style="color: white" @click="proximaPagina">Next page</a>
          <ul class="pagination-list">
            <li>
              <a
                class="pagination-link" style="color: white"
                aria-label="Page 1"
                aria-current="page"
                @click="atualizarPaginaAtual(0)"
                >1</a
              >
            </li>
            <li>
              <a
                class="pagination-link" style="color: white"
                aria-label="Goto page 2"
                @click="atualizarPaginaAtual(1)"
                >2</a
              >
            </li>
            <li>
              <a
                class="pagination-link" style="color: white"
                aria-label="Goto page 3"
                @click="atualizarPaginaAtual(2)"
                >3</a
              >
            </li>
          </ul>
        </nav>
      </div>

  ```
</details>

<details>
  <summary>Adição do Logo no cabeçalho</summary>
  
  ```javascript
      <nav class="navbar" role="navigation" aria-label="main navigation">
      <div class="navbar-brand">
        <a class="navbar-item">
          <img src="./assets/logo.svg" width="100">
        </a>
        <a class="navbar-item" href="/">Home</a>
        <a class="navbar-item" href="/new/account">Criar conta</a>
        <!-- <a class="navbar-item" href="/filtrar-clientes">CSV</a> -->
        <a class="navbar-item" href="/login">Login</a>
      </div>
      <div class="navbar-menu">
        <!-- navbar start, navbar end -->
      </div>
    </nav>
  ```
</details>

<details>
  <summary>Desenvolvimento da tela de Dashboard (front-end)</summary>
  
  ```javascript
  <script>
import axios from "axios";
import VueChart from "../components/VueChart.vue";

export default {
  components: {
    VueChart,
  },

  props: {
    listaCSV: {
      type: Array,
      default: []
    },
  },

  data() {
    return {
      dadosChart1: [],
      dadosChart2: [],
      dadosChart3: [],

      labelsChart1: [],
      labelsChart2: [],
      labelsChart3: [],

      optionsChart1: {},
      optionsChart2: {},
      optionsChart3: {},

      valorteste: 20,
    };
  },

  methods: {

    tratarGrafico1() {
      let masculino = 0;
      let feminino = 0;
      let outros = 0;

      this.listaCSV.forEach((linhaExcel) => {
        if (linhaExcel.gender === "feminino") {
          feminino += 1;
        } else if (linhaExcel.gender === "masculino") {
          masculino += 1;
        } else {
          outros += 1;
        }
      });

      let data = [feminino, masculino, outros];

      this.labelsChart1 = ['feminino', 'masculino', 'outros'];
      this.optionsChart1 = {
        responsive: true
      };
      this.dadosChart1 = [
        {
          label: "Comparação de compra entre os gêneros",
          backgroundColor: "rgba(152,120,200,0.1)",
          borderColor: "rgba(152, 120, 200, 1)",
          borderWidth: "2",
          borderRadius: 2,
          data,
          indexAxis: "x",
        },
      ];
    },

    tratarGrafico2() {
      let produtosPorGenero = [];

      console.log(this.listaCSV)
      this.listaCSV.forEach((linhaExcel) => {
        let categoria  = linhaExcel.category?.toLowerCase();
        let genero     = linhaExcel.gender?.toLowerCase();
        let quantidade = linhaExcel.quantity ?? 0;

        if (!produtosPorGenero[genero]) {
          produtosPorGenero[genero] = [];
        }
        
        if (!produtosPorGenero[genero][categoria] && produtosPorGenero[genero][categoria] !== 0) {
          produtosPorGenero[genero][categoria] = quantidade;
        } else {
          produtosPorGenero[genero][categoria] += quantidade;
        }
      });
      
      let maxMasculino;
      let maxFeminino;
      let maxOutros;
      let produtos = produtosPorGenero['masculino']
      Object.keys(produtos).forEach(key => {
        if (!maxMasculino) {
          maxMasculino = { nomeProduto: key, quantidade: produtos[key] }
        } else if (maxMasculino.quantidade < produtos[key]) {
          let quantidade = produtos[key];
          maxMasculino = { nomeProduto: key, quantidade }
        }
      })

      produtos = produtosPorGenero['feminino'];
      Object.keys(produtos).forEach(key => {
        if (!maxFeminino) {
          maxFeminino = { nomeProduto: key, quantidade: produtos[key] }
        } else if (maxFeminino.quantidade < produtos[key]) {
          let quantidade = produtos[key];
          maxFeminino = { nomeProduto: key, quantidade }
        }
      })

      produtos = produtosPorGenero['outros'];
      Object.keys(produtos).forEach(key => {
        if (!maxOutros) {
          maxOutros = { nomeProduto: key, quantidade: produtos[key] }
        } else if (maxOutros.quantidade < produtos[key]) {
          let quantidade = produtos[key];
          maxOutros = { nomeProduto: key, quantidade }
        }
      })
      
      let data = [
        maxFeminino.quantidade,
        maxMasculino.quantidade,
        maxOutros.quantidade
      ];

      this.labelsChart2 = [`mulheres: ${maxFeminino.nomeProduto}`, `homens: ${maxMasculino.nomeProduto}`, `outros: ${maxOutros.nomeProduto}`];
      
      this.optionsChart2 = {
        responsive: true,
        maintainAspectRatio: false
      };

      this.dadosChart2 = [
        {
          label: [maxFeminino.nomeProduto, maxMasculino.nomeProduto, maxOutros.nomeProduto],
          backgroundColor: ["rgba(250, 120, 200, 0.1)", "rgba(100, 100, 200, 0.1)", "rgba(152, 250, 200, 0.1)"],
          borderColor: ["rgba(250, 120, 200, 1)", "rgba(100, 100, 200, 1)", "rgba(152, 250, 200, 1)"],
          data,
        },
      ];
    },

    tratarGrafico3() {
      let listaGastosPorRegiao = [];

      this.listaCSV.forEach((linhaExcel) => {
        let regiao = linhaExcel.region?.toLowerCase();
        let genero = linhaExcel.gender?.toLowerCase();
        let gasto  = linhaExcel.spent ?? 0;
        if (!listaGastosPorRegiao[genero]) {
          listaGastosPorRegiao[genero] = { centro: 0, leste: 0, norte: 0, oeste: 0, sudeste: 0, sul: 0 };
        } else {
          listaGastosPorRegiao[genero][regiao] += gasto;
        }
      });

      let data = [
        listaGastosPorRegiao['feminino'],
        listaGastosPorRegiao['masculino'],
        listaGastosPorRegiao['outros'],
      ];

      let generos = [
        {label: 'feminino', color: 'rgba(250, 120, 200, 0.5)', borderColor: 'rgba(250, 120, 200, 1)'}, 
        {label: 'masculino', color: 'rgba(100, 100, 200, 0.5)', borderColor: 'rgba(100, 100, 200, 1)'}, 
        {label: 'outros', color: 'rgba(152, 250, 200, 0.5)', borderColor: 'rgba(152, 250, 200, 1)'}
      ];

      this.labelsChart3 = ['centro', 'leste', 'norte', 'oeste', 'sudeste', 'sul'];
      
      this.optionsChart3 = {
        responsive: true,
        maintainAspectRatio: false
      }

      this.dadosChart3 = data.map((dadosRegiao, index) => ({
        label: generos[index].label,
        backgroundColor: generos[index].borderColor,
        borderColor: generos[index].color,
        data: [
          dadosRegiao['centro'],
          dadosRegiao['leste'],
          dadosRegiao['norte'],
          dadosRegiao['oeste'],
          dadosRegiao['sudeste'],
          dadosRegiao['sul']
        ],
      }))
    },
  },

  beforeMount() {
    this.tratarGrafico1();
    this.tratarGrafico2();
    this.tratarGrafico3();
  },
};
</script>

<template>
  <div class="pageContainer">
    <div class="chartContainer">
      <div class="chartBox">
        <p>Soma de todos os produtos por gênero</p>
        <vue-chart
          v-if="dadosChart1.length > 0"
          :dataset="this.dadosChart1"
          :labels="this.labelsChart1"
        ></vue-chart>
      </div>
      
      <div class="chartBox">
        <p>Produto mais vendido por gênero</p>
        <vue-chart
          v-if="dadosChart2.length > 0"
          :dataset="this.dadosChart2"
          :labels="this.labelsChart2"
          :chartOptions="this.optionsChart2"
          :height="178"
          type="doughnut"
        ></vue-chart>  
      </div>

      <div id="teste" class="chartBox" style="width: 100%">
        <p>Valor gasto por gênero para cada região</p>
        <vue-chart
          v-if="dadosChart3.length > 0"
          :dataset="this.dadosChart3"
          :labels="this.labelsChart3"
          :chartOptions="this.optionsChart3"
          :height="250"
          :width="350"
          type="line"
        ></vue-chart>
      </div>
    </div>
  </div>
</template>

<style>
.pageContainer {
  padding: 10px;
  width: 100%;
}

.chartContainer {
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}

.chartBox {
  height: 40%;
  width: 48%;
  background-color: rgb(48, 46, 54);
  /* background-color: white; */
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
}

.chartBox > p {
  text-align: center;
}
</style>

  ```
</details>

<details>
  <summary>Filtros na tela Filtrar clientes, que são: Gênero, Região, Categoria do sapato e Cor</summary>
  
  ```javascript
  </div>

  <div style="display:flex; justify-content:space-evenly">
    <div v-if="listaCSV.length > 0" style="display: flex; flex-wrap: wrap; margin: 20px">
      <div class="field" style="width: 200px">
        <label class="label" style="color: white; font-size: 0.90rem">Gênero</label>
        <div class="select" style="width: 100%">
          <select ref="filtroGenero" style="width: 100%" @change="filtrarDados">
            <option>Selecione</option>
            <option>Masculino</option>
            <option>Feminino</option>
            <option>Outros</option>
          </select>
        </div>
      </div>
    </div>

    <div v-if="listaCSV.length > 0" style="display: flex; margin: 20px">
      <div class="field" style="width: 200px">
        <label class="label" style="color: white; font-size: 0.90rem">Região</label>
        <div class="select" style="width: 100%">
          <select ref="filtroRegiao" style="width: 100%" @change="filtrarDados">
            <option>Selecione</option>
            <option>Centro</option>
            <option>Norte</option>
            <option>Leste</option>
            <option>Sudeste</option>
            <option>Sul</option>
            <option>Oeste</option>
          </select>
        </div>
      </div>
    </div>

    <div v-if="listaCSV.length > 0" style="display: flex; margin: 20px">
      <div class="field" style="width: 200px">
        <label class="label" style="color: white; font-size: 0.90rem">Categoria do sapato</label>
        <div class="select" style="width: 100%">
          <select ref="filtroCategoriaSapato" style="width: 100%" @change="filtrarDados">
            <option>Selecione</option>
            <option>Sapatos Sociais</option>
            <option>Tênis</option>
            <option>Sapatênis</option>
            <option>Bota</option>
            <option>Sandália</option>
            <option>Rasteirinha</option>
            <option>Sapatilha</option>
            <option>Tamanco</option>
            <option>Outros Tipos</option>
          </select>
        </div>
      </div>
    </div>
    <div v-if="listaCSV.length > 0" style="display: flex; margin: 20px">
      <div class="field" style="width: 200px">
        <label class="label" style="color: white; font-size: 0.90rem">Cor</label>
        <div class="select" style="width: 100%">
          <select ref="filtroCor" style="width: 100%" @change="filtrarDados">
            <option>Selecione</option>
            <option>Bege</option>
            <option>Preto</option>
            <option>Branco</option>
            <option>Amarelo</option>
            <option>Azul</option>
            <option>Vermelho</option>
            <option>Verde</option>
            <option>Rosa</option>
            <option>Marrom</option>
            <option>Cinza</option>
          </select>
        </div>
      </div>
    </div>
  </div>

  ```
</details>

<details>
  <summary>Funcionalidade de Gerar Relatório</summary>
  
  ```javascript

{  methods: {
    
    gerarRelatorio: async () => {
      

      const headers = {
        "Content-Type": "multipart/form-data",
        Authorization: `Bearer ${localStorage.getItem("userToken")}`,
      };

      const result = await axios.get("http://localhost:8081/api/csv/csvdata", { headers })

      let dadosVendaPorProduto = [];
      result.data.reduce((listaSomaAgrupada, linhaExcel) => {
        if (!listaSomaAgrupada[linhaExcel.category]) {
          listaSomaAgrupada[linhaExcel.category] = { category: linhaExcel.category, quantidade: 0, valorTotal: 0 };
          dadosVendaPorProduto.push(listaSomaAgrupada[linhaExcel.category])
        }
        listaSomaAgrupada[linhaExcel.category].quantidade += linhaExcel.quantity;
        listaSomaAgrupada[linhaExcel.category].valorTotal += linhaExcel.spent;
        return listaSomaAgrupada;
      })

      dadosVendaPorProduto = dadosVendaPorProduto.filter(linha => linha.category !== null);
      dadosVendaPorProduto = dadosVendaPorProduto.map(linha => ({
        ...linha,
        valorTotal: `R$ ${linha.valorTotal}`
      }))
      console.log(dadosVendaPorProduto);

      autoTable(doc, {
        head: [['Categoria', 'Quantidade comprada', 'Valor total']],
        body: dadosVendaPorProduto.map(linha => [linha.category, linha.quantidade, linha.valorTotal]),
      })
      doc.addPage();
      doc.text(20, 20, 'Do you like that?');
      doc.save("relatorio_lefoot.pdf");
    }

  }
};
</script>

      <p class="control">
        <button class="button is-outlined is-primary" @click="() => this.modoVisualizacao = 'tabela'">tabela</button>
      </p>
      <p class="control">
        <button class="button is-outlined is-primary" @click="() => this.gerarRelatorio()">Gerar relatório</button>
      </p>
    </div>

    <tela-dashboard-view v-if="this.modoVisualizacao === 'dashboard'" />


  ```
</details>


#### Hard Skills Efetivamente Desenvolvidas
* HTML, CSS, JavaScript

#### Soft Skills Efetivamente Desenvolvidas
* Confiança
* Lógica de programação
