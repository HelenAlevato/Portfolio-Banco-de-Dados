## Meu Quarto API  📚

#### Em 2022-1 (API 4)
Trabalhei no projeto da API do quarto semestre como desenvolvedora front-end. [GitLab do projeto.](https://gitlab.com/vueforce1/lefoot)<br> 
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
Fiz os desenhos da tela pelo figma e o modo de navegação, como ficaria no projeto final.
Fiz algumas coisas no back-end também ...
Fiz ...

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
 

  ```
</details>

<details>
  <summary>Paginação da tela Filtrar clientes</summary>
  
  ```javascript

  ```
</details>

<details>
  <summary>Adição do Logo no cabeçalho</summary>
  
  ```javascript

  ```
</details>

<details>
  <summary>Desenvolvimento da tela de Dashboard (front-end)</summary>
  
  ```javascript
  - mock
  - implementação da lógica dos gráficos

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
