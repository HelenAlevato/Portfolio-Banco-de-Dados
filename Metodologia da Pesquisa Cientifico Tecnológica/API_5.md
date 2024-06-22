## Meu Quinto API  📚

#### Em 2022-2 (API 5)
Trabalhamos no projeto da API do quinto semestre como desenvolvedora back-end. Com o curso de Manutenção de Aeronaves. [GitHub do projeto.](https://github.com/EquipeFatec/persuance-frontend)<br> 


![image](https://github.com/HelenAlevato/Portfolio-Banco-de-Dados/assets/61571753/0d2cd153-a4b0-44ba-a314-72b99b057230)


- **Nome do Grupo:** Sanja valley
- **Nome do Software:**  Persuance
- **Visão do Produto:** Este projeto visa desenvolver uma aplicação para utilização da norma, exibindo as palavras aprovadas ou não aprovadas para consulta e verificação de textos.
     
 - **Objetivo do Produto:** 
	 - A norma STE é utilizada pelos fabricantes de aviões e componentes aeronáuticos com a proposta de escrever em inglês utilizando não mais que 900 palavras (todos os fabricantes utilizam). Para a documentação das aeronaves, é necessário realizar uma verificação das palavras aprovadas para que esteja conforme a norma. Atualmente, no curso de Manutenção de Aeronaves, esta busca é realizada por meio de uma planilha que apresenta as palavras e suas características.
  
- **Problema (Desafio):** 

	- O desafio era criar um sistema que automatizasse a verificação de conformidade com a norma STE (Simplified Technical English) para documentação de aeronaves, especialmente para o curso de Manutenção de Aeronaves da Fatec. Atualmente, a verificação é realizada manualmente através de uma planilha que lista as palavras aprovadas e suas características, o que é um processo demorado e suscetível a erros.

- **Proposta:**
	- Criado pela equipe Sanja Valley, este projeto visa desenvolver uma aplicação para utilização da norma, exibindo as palavras aprovadas ou não aprovadas para consulta e verificação de textos.
	

#### Tecnologias Utilizadas 🛠
- Front-end: CSS, HTML, JavaScript, VueJS, PrimeVue, Visual Studio Code
- Back-end: Java, SpringBoot, Gradle, IntelliJ IDE
- Banco de Dados: MySQL

## Contribuições Pessoais 👩
Nesse trabalho fiquei como Team Dev, responsavel pela parte de back-end. 

**Desenvolvimento:** 
<details>
  <summary>Upload de arquivo</summary>
	
	Nessa tela foi desenvolvida a funcionalidade de upload de arquivo, para conseguir subir as palavras necessárias para o uso do sistema. 
  
  ```javascript
  <template>
  <Toast />
  <main>
    <div id="painelRedefinir">
      <h3 style="font-size: 30px">Importação de dados</h3>
      <div style="display: flex; justify-content: center; margin: 30px">
        <FileUpload mode="basic" name="file" accept=".csv" url="http://localhost:8081/api/csv/upload"
          :maxFileSize="1000000" @upload="onUpload" :auto="true" multiple="false">
          <template #empty>
            <p>Drag and drop files to here to upload.</p>
          </template>
        </FileUpload>
      </div>
    </div>
  </main>
</template>

<script>
// import axios from "axios";
import { onBeforeMount } from "@vue/runtime-core";
import FileUpload from "primevue/fileupload";
import Toast from "primevue/toast";
import Button from "primevue/button";

export default {
  data() {
    return {
      modoVisualizacao: "",
      listaCSV: [],
    };
  },
  name: "TelaUpload",
  components: {
    FileUpload,
    Button,
    Toast
  },

  methods: {
    onUpload(event) {
      this.$toast.add({
        severity: "success",
        summary: "Success",
        detail: "Upload concluído",
        life: 3000,
      });
    },
  },
};
</script>


<style scoped>
main {
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 20px;
}

#painelRedefinir {
  width: 100%;
  min-width: 20%;
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: white;
  margin-top: 60px;
  display: flex;
  flex-direction: column;
  background-color: rgb(48, 46, 54);
  padding: 20px;
  border-radius: 10px;
}
</style>
  ```
</details>

<details>
  <summary>Tela de filtros</summary>
	
	Nessa tela foi desenvolvida a funcionalidade de  filtrar as palavras com alguns critérios, fazendo parte do front-end e do back-end.
  
  ```javascript
  <template>
  <div class="list">
    <Menu></Menu>

    <h1 class="titulo">Tela de Filtros</h1>
    <DataTable
      :value="words"
      :paginator="true"
      :rows="5"
      :rowHover="true"
      v-model:filters="filters"
      :loading="loading"
      :rowsPerPageOptions="[2, 5, 10, 25, 50]"
      :globalFilterFields="['palavra','traducao']"
      dataKey="id"
      showGridLines
      filterDisplay="menu"
      paginatorTemplate="FirstPageLink PrevPageLink PageLinks NextPageLink LastPageLink CurrentPageReport RowsPerPageDropdown"
      currentPageReportTemplate="Exibindo {first} à {last} do total de {totalRecords} registros"
      responsiveLayout="scroll"
    >
      <template #header>
        <div class="flex justify-content-center align-items-center">
          <span class="p-input-icon-left">
            <i class="pi pi-search" />
            <InputText v-model="filters['global'].value" placeholder="Buscar palavra-chave" />
          </span>
        </div>
      </template>
      <template #empty>Nenhuma palavra disponivel na base de dados</template>
      <template #loading>Carregando palavras</template>
      <Column field="palavra" header="Palavra" sortable style="min-width: 14rem">
        <template #body="{ data }">
          {{ data.palavra }}
        </template>
        <template #filter="{ filterModel }">
          <InputText
            type="text"
            v-model="filterModel.value"
            class="p-column-filter"
            placeholder="Pesquisar por letra"
          />
        </template>
      </Column>
      <Column field="traducao" sortable header="Tradução">
        <template #body="{ data }">
          {{ data.traducao }}
        </template>
        <template #filter="{ filterModel }">
          <InputText
            type="text"
            v-model="filterModel.value"
            class="p-column-filter"
            placeholder="Pesquisar"
          />
        </template>
      </Column>
      <Column field="aprovada" sortable header="Aprovada">
        <template #body="{ data }">
          <span :class="'badge status' + (data.aprovada === 'sim' ? '-aprovado' : '')">
            {{ data.aprovada }}
          </span>
        </template>
        <template #filter="{ filterModel }">
          <InputText
            type="text"
            v-model="filterModel.value"
            class="p-column-filter"
            placeholder="Pesquisar"
          />
        </template>
      </Column>
      <Column field="significado" sortable header="Significado">
        <template #body="{ data }">
          {{ data.significado }}
        </template>
        <template #filter="{ filterModel }">
          <InputText
            type="text"
            v-model="filterModel.value"
            class="p-column-filter"
            placeholder="Pesquisar"
          />
        </template>
      </Column>
      <Column field="conjucacao" sortable header="Conjugação">
        <template #body="{ data }">
          {{ data.conjucacao }}
        </template>
        <template #filter="{ filterModel }">
          <InputText
            type="text"
            v-model="filterModel.value"
            class="p-column-filter"
            placeholder="Pesquisar"
          />
        </template>
      </Column>
      <Column field="exemploAprovado" sortable header="Exemplo de uso">
        <template #body="{ data }">
          {{ data.exemploAprovado }}
        </template>
        <template #filter="{ filterModel }">
          <InputText
            type="text"
            v-model="filterModel.value"
            class="p-column-filter"
            placeholder="Pesquisar"
          />
        </template>
      </Column>
      <Column field="classeGramatical" sortable header="Classe Gramatical">
        <template #body="{ data }">
          {{ data.classeGramatical }}
        </template>
        <template #filter="{ filterModel }">
          <Dropdown v-model="filterModel.value" :options="classesGramaticais" placeholder="Any" class="p-column-filter" :showClear="true">
        </Dropdown>
        </template>
      </Column>
      <Column field="categoria" sortable header="Categoria">
        <template #body="{ data }">
          {{ data.categoria }}
        </template>
        <template #filter="{ filterModel }">
          <InputText
            type="text"
            v-model="filterModel.value"
            class="p-column-filter"
            placeholder="Pesquisar"
          />
        </template>
      </Column>
      <Column field="revisao" sortable header="Revisão">
        <template #body="{ data }">
          {{ data.revisao }}
        </template>
        <template #filter="{ filterModel }">
          <InputText
            type="text"
            v-model="filterModel.value"
            class="p-column-filter"
            placeholder="Pesquisar"
          />
        </template>
      </Column>
    </DataTable>
  </div>
</template>

<script>
import DataTable from "primevue/datatable";
import Column from "primevue/column";
import ColumnGroup from "primevue/columngroup"; //optional for column grouping
import Row from "primevue/row"; //optional for row
import InputText from "primevue/inputtext";
import Dropdown from "primevue/dropdown";
import axios from "axios";
import { FilterMatchMode } from "primevue/api";
import PalavraService from "../services/PalavraService";
import Menu from '../components/Menu.vue';

export default {
  name: "PalavraListView",
  components: {
    DataTable,
    Column,
    InputText,
    ColumnGroup,
    Row,
    Dropdown,
    Menu
  },
  data() {
    return {
      loading: true,
      words: null,
      filters: {
        'global': { value: null, matchMode: FilterMatchMode.STARTS_WITH },
        'palavra': { value: null, matchMode: FilterMatchMode.STARTS_WITH },
        'traducao': { value: null, matchMode: FilterMatchMode.STARTS_WITH },
        'aprovada': { value: null, matchMode: FilterMatchMode.STARTS_WITH },
        'significado': { value: null, matchMode: FilterMatchMode.STARTS_WITH },
        'conjucacao': { value: null, matchMode: FilterMatchMode.STARTS_WITH },
        'exemploAprovado': { value: null, matchMode: FilterMatchMode.STARTS_WITH },
        'classeGramatical': { value: null, matchMode: FilterMatchMode.EQUALS },
        'categoria': { value: null, matchMode: FilterMatchMode.STARTS_WITH },
        'revisao': { value: null, matchMode: FilterMatchMode.STARTS_WITH },
      },
      classesGramaticais:[
        "Substantivo",
        "Advérbio",
        "Adjetivo",
        "Preposição",
        "Verbo",
        "Conjunção",
        "Pronome",
        "Artigo"
      ]
    };
  },
  palavraService: null,
  created() {
    this.palavraService = new PalavraService();
  },
  mounted() {
    this.palavraService.getPalavras().then(data => {
      this.words = data;
    }).finally(() => {
      this.loading = false;
    });
  },
};
</script>

<style>

@import "../style/PalavraList.css"

</style>
  ```
</details>

<details>
  <summary>Ação botão sair</summary>
	
	Funcionalidade do botão sair
  
  ```javascript
{
	label: 'Sair',
	icon: 'pi pi-times',
	command: () => {
		this.$toast.add({ severity: 'success', summary: 'Logout', detail: 'Logout Realizado', life: 3000});
		localStorage.removeItem("userToken");
		window.location.href="/#/home";
}
  ```
</details>


<div align="center">

**Hard Skills**
|**Tecnologia/Metodologia**|**Classificação**      |
|--------------------------|-----------------------|
|HTML                      |Sei fazer com Autonomia|
|CSS                       |Sei fazer com Autonomia|
|JavaScript                |Sei fazer com Ajuda    |
|Git                       |Sei fazer com Ajuda    |
|GitHub                    |Sei fazer com Ajuda    |
|Vue.js                    |Sei fazer com Ajuda    |
|Jira Software             |Sei fazer com Ajuda    |
|Java                      |Entendi                |
|OracleSQL                 |Entendi                |



**Soft Skills**
|**Habilidade**     |**Descrição**        |
|-------------------|---------------------|
|Organização|Capacidade de planejar e gerenciar tarefas de forma eficiente.|
|Trabalho em Equipe|Habilidade de colaborar e comunicar efetivamente com outros membros da equipe para alcançar objetivos comuns.|
|Proatividade|Iniciativa para identificar e abordar problemas, capacidade de buscar oportunidades de melhoria sem a necessidade de supervisão.|
|Confiança|Autoconfiança e a capacidade de confiar nos próprios conhecimentos e habilidades, bem como nos outros membros da equipe.|
|Lógica de programação|Capacidade de pensar logicamente e resolver problemas de forma estruturada e eficaz usando algoritmos e técnicas de programação.|

</div>

