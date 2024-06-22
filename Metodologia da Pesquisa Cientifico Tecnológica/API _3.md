## Meu Terceiro API  📚

#### Em 2021-1 (API 3)
Trabalhamos no projeto da API com o Parceiro Embraer.  [GitHub do projeto.](https://github.com/HelenAlevato/14bis)<br> 


![image](https://github.com/HelenAlevato/Portfolio-Banco-de-Dados/assets/61571753/7133976c-97c4-4945-9712-0c6677892b75)


- **Nome do Grupo:** Finger One
- **Nome do Software:**  14 BIS
- **Visão do Produto:** Fornecer suporte para a criação de um software, onde o usuário terá uma facilidade em customizar, controlar e revisar documentos formados por fragmentos armazenados em arquivos PDF.
     
 - **Objetivo do Produto:** 
	  -   Sanar e simplificar a geração de fragmentos que irão compor o armazenamento em PDF.
  
- **Problema (Desafio):** 

	- Desenvolver um sistema que permita customizar, controlar e revisar documentos formados por fragmentos armazenados em arquivos PDF, usando regras especificas para gerar o documento final.

- **Proposta:**

	-   Após contato com a empresa, levantamos que eles querem simplificar o processo e ser mais assertivo. Sendo assim será desenvolvido um sistema simples e objetivo, fazendo com que seja ágil e a taxa de erro seja menor. <br>

#### Tecnologias Utilizadas 🛠
- [GitHub](https://trello.com/b/EW0XA8qH/finger-one)
 - [Trello](https://trello.com/pt-BR)
 - [Adobe XD](https://www.adobe.com/br/products/xd.html)
 - [StackEdit]( https://stackedit.io/)
 - [PostgreSQL](https://www.postgresql.org/)
 - [Intellij](https://www.jetbrains.com/pt-br/idea/)
 - [Java](https://www.oracle.com/br/java/technologies/javase/javase-jdk8-downloads.html)
 - [Eclipse](https://www.eclipse.org/downloads/)
 - [VSCode](https://code.visualstudio.com/download)
 - [React](https://react-cn.github.io/react/downloads.html)
 - [Carbon](https://www.carbondesignsystem.com/designing/kits/sketch/)
 - [Postman](https://www.postman.com/downloads/)
 - [Spring boot](https://spring.io/)


## Contribuições Pessoais 👩
Dentro das contribuições pessoais eu fiquei responsável por ser P.O e membro da equipe do front-end. Com explicarei abaixo:

**P.O:**

Na experiência como P.O., aprendi muito. É um cargo de grande responsabilidade e essencial para o bom andamento do projeto. Nesse papel, estive em contato direto com o cliente, sempre tentando entender suas necessidades e o que nós, alunos do terceiro semestre, podíamos desenvolver com o conhecimento que tínhamos e estávamos adquirindo. Enfrentei muitos desafios e percebi que não tenho o perfil ideal para ser P.O. Com o grupo, realizava pelo menos duas reuniões semanais. Conseguimos documentar bem os requisitos esperados, e assim as atividades foram distribuídas entre a equipe de Front-end e a de Back-end/Banco de Dados.

**Desenvolvimento:**  

- Retornar codelist salvo no banco de dados
- Permitir arquivo para extração do codelist pelo FrontEnd
- Atualização da proposta Sprint 2
- Adição da Aba "LEP" na página de Codelist
- Adição da entidade Manual
- Adição do manual ao passar o Codelist
- Pequenas atualizações visuais na interface
- Envio do nome do manual na inserção do codelist
- Tabela Manual: Retornar todos os manuais cadastrados
- Controller para busca dos manuais
- Adição da Tela de Edição de Blocos do Codelist
- Ajuste na configuração do caminho do PDF
- Melhorias na página do codelist e busca de PDFs com base na aplicabilidade
- Busca de todas as páginas pelo bloco e pelo codigo

Código de exemplo na construção das telas

<details>
  <summary>Codelist</summary>
	
	Essa é a funcionalidade da tela chamada Codelist, onde podemos edição dos blocos e gerenciamento dos arquivos.
  
  ```java
  @CrossOrigin("http://localhost:3000")
	@Controller
	@RequestMapping("/api/codelist")
	@Api(value = "Codelist")
	public class CodeListController {

		@Autowired
		ExcelService fileService;

		@Autowired
		PdfPageService pdfPageService;

		@Autowired
		CodeListRepository repository;

		@PostMapping("/upload")
		public ResponseEntity<ResponseMessage> uploadCodelist(@RequestParam("file") MultipartFile file,
				@RequestParam("manualName") String manualName) {
			String message = "";

			if (ExcelHelper.hasExcelFormat(file)) {
				Manual manual = new Manual();
				manual.setNome(manualName);
				manual.setDate(new Date());

				try {
					pdfPageService.createNewManualDirectory(manualName);
					fileService.save(file, manual);

					message = "Uploaded the file successfully: " + file.getOriginalFilename();
					return ResponseEntity.status(HttpStatus.OK).body(new ResponseMessage(message));
				} catch (Exception e) {
					message = "Could not upload the file: " + file.getOriginalFilename() + "!";
					return ResponseEntity.status(HttpStatus.EXPECTATION_FAILED).body(new ResponseMessage(message));
				}
			}

			message = "Please upload an excel file!";
			return ResponseEntity.status(HttpStatus.BAD_REQUEST).body(new ResponseMessage(message));
		}

		@PostMapping("/delete")
		public ResponseEntity<ResponseMessage> deleteCodelists(@RequestParam("idsToDelete") String idsToDelete) {
			String message = "";
			try {
				String[] ids = idsToDelete.split(",");
				for (String id : ids) {
					repository.deleteById(Long.valueOf(id));
				}

				message = "Codelists succesfully deleted";
				return ResponseEntity.status(HttpStatus.OK).body(new ResponseMessage(message));
			} catch (Exception e) {
				message = "Error while deleting codelists";
				return ResponseEntity.status(HttpStatus.EXPECTATION_FAILED).body(new ResponseMessage(message));
			}
		}

		@GetMapping
		public ResponseEntity<List<CodeList>> getAllCodelists() {
			try {
				List<CodeList> codelist = fileService.getAllCodelists();

				if (codelist.isEmpty()) {
					return new ResponseEntity<>(HttpStatus.NO_CONTENT);
				}

				return new ResponseEntity<>(codelist, HttpStatus.OK);
			} catch (Exception e) {
				return new ResponseEntity<>(null, HttpStatus.INTERNAL_SERVER_ERROR);
			}
		}

		@GetMapping("/manual/{nomeManual}")
		public ResponseEntity<List<CodeList>> getCodelistByManual(@PathVariable("nomeManual") String nomeManual) {
			try {
				List<CodeList> codelist = fileService.getAllCodelistsByManualName(nomeManual);

				if (codelist.isEmpty()) {
					return new ResponseEntity<>(HttpStatus.NO_CONTENT);
				}

				return new ResponseEntity<>(codelist, HttpStatus.OK);
			} catch (Exception e) {
				return new ResponseEntity<>(null, HttpStatus.INTERNAL_SERVER_ERROR);
			}
		}
	}
	
  ```
</details>
	
<details>
  <summary>Tela de Edição de Blocos do Codelist</summary>
	
	Tela da Codelist, onde os Blocos da Codelist podem ser editados, excluidos ou adicionado.
  
  ```java
	import { Add16, Add20, Add32, ArrowLeft32, MisuseOutline16 } from "@carbon/icons-react"
	import {
		Button,
		DataTable,
		Table,
		TableBody,
		TableCell,
		TableHead,
		TableHeader,
		TableRow,
		TableToolbar,
		TableToolbarContent,
		Form,
		TextInput,
		TableContainer,
		TableToolbarSearch
	} from "carbon-components-react"
	import { useEffect, useState } from "react"
	import { useHistory, useParams } from "react-router-dom"

	const headers = [
		{
			style: { width: '10%' },
			key: 'secao',
			header: 'Nº Seção',
		},
		{
			style: { width: '12%' },
			key: 'subSecao',
			header: 'Nº Sub Seção',
		},
		{
			style: { width: '10%' },
			key: 'bloco',
			header: 'Nº Bloco',
		},
		{
			key: 'blockName',
			header: 'Block Name',
		},
		{
			style: { width: '10%' },
			key: 'code',
			header: 'Code',
		},
		{
			key: 'remarks',
			header: 'Remarks',
		},
		{
			key: '',
			header: '',
		},
	]


	const EditCodeListPage = () => {
		var [codelist, setCodelist] = useState([]);
		var [fetchedCodelist, setFetchedCodelist] = useState([]);
		var [isLoaded, setLoaded] = useState(false);

		var [blocosRemovidos, setBlocosRemovidos] = useState([]);
		const history = useHistory();

		let nomeManual = useParams().nomeManual;

		useEffect(async () => {
			if (!isLoaded) {
				let response = await fetch(`http://localhost:8585/api/codelist/manual/${nomeManual}`).then(response => response.json());
				setFetchedCodelist(response);
				setCodelist(fetchedCodelist);
				setLoaded(true);
			}
		})

		const filtrarCodelist = (e) => {
			// let textoDeFiltro = e.target.value
			// codelist = fetchedCodelist
			// setCodelist(codelist.filter(bloco => bloco.nome.includes(textoDeFiltro)))
		}

		const removerBloco = (e, index) => {
			setCodelist(codelist.filter((bloco, blocoIndex) => {
				if (blocoIndex === index) {
					blocosRemovidos.push(bloco)
				}
				return blocoIndex !== index
			}))
			setBlocosRemovidos(blocosRemovidos)
		}

		const onBlocoChange = (value, blocoIndex) => {
			this.setState({
				name: value
			});
		}

		const updateCodelist = (blocoAlterado, blocoIndex) => {
			let novoCodelist = codelist.map((bloco, index) => {
				if (blocoIndex === index) {
					bloco = blocoAlterado;
				}
				return bloco;
			})
			setCodelist(novoCodelist);
		}

		const handleCancel = () => {
			history.push(`/CodeList/${nomeManual}`)
		}

		const handleSave = async () => {
			await handleDeleteBlocks()
		}

		const handleDeleteBlocks = async () => {
			let idsToDelete = [];
			idsToDelete = blocosRemovidos.map(bloco => bloco.id).join(",");

			console.log("ids a serem deletados", idsToDelete)

			const formData = new FormData();
			formData.append('idsToDelete', idsToDelete);

			const opcoesRequest = { method: 'POST', body: formData };

			await fetch('http://localhost:8585/api/codelist/delete', opcoesRequest)
				.catch(err => console.log(err))
				.then(response => response.json())
				.then(data => history.push(`/CodeList/${nomeManual}`)
			);
		}

		return (
			<div>
				<ArrowLeft32 style={{ cursor: "pointer" }} onClick={() => history.goBack()} />
				<Form>
					<DataTable rows={codelist} headers={headers}>
						{({
							rows,
							headers,
							getHeaderProps,
							getRowProps,
							getTableProps,
							onInputChange
						}) => (

							<TableContainer title={`Edição do ${nomeManual}`} description="Edite as linhas do codelist">
								<TableToolbar>
									<TableToolbarContent>
										<TableToolbarSearch onChange={filtrarCodelist} />
									</TableToolbarContent>
								</TableToolbar>
								<Table {...getTableProps()} size='short'>
									<TableHead style={{ fontSize: '10px' }}>
										<TableRow>
											{headers.map(header => (
												<TableHeader
													style={header.style}
													key={header.key}
													{...getHeaderProps({ header })}>
													{header.header}
												</TableHeader>
											))}
										</TableRow>
									</TableHead>
									<TableBody>
										{codelist.map((bloco, index) => (

											<TableRow key={bloco.id} style={{ fontSize: '5px' }}>
												<TableCell>
													<TextInput
														size="sm"
														style={{ fontSize: '0.65rem', padding: 0, textAlign: 'center' }}
														placeholder=""
														value={bloco.secao}
														onChange={e => { bloco.secao = e.target.value; updateCodelist(bloco, index) }}
													/>
												</TableCell>
												<TableCell>
													<TextInput
														size="sm"
														style={{ fontSize: '0.65rem', padding: 0, textAlign: 'center' }}
														value={bloco.subSecao ? bloco.subSecao : '-'}
														onChange={e => { bloco.subSecao = e.target.value; updateCodelist(bloco, index) }}
													/>
												</TableCell>
												<TableCell>
													<TextInput
														size="sm"
														style={{ fontSize: '0.65rem', padding: 0, textAlign: 'center' }}
														value={bloco.bloco}
														onChange={e => { bloco.bloco = e.target.value; updateCodelist(bloco, index) }}
													/>
												</TableCell>
												<TableCell>
													<TextInput
														size="sm"
														style={{ fontSize: '0.65rem' }}
														value={bloco.nomeBloco}
														onChange={e => { bloco.nomeBloco = e.target.value; updateCodelist(bloco, index) }}
													/>
												</TableCell>
												<TableCell>
													<TextInput
														size="sm"
														style={{ fontSize: '0.65rem', padding: 0, textAlign: 'center' }}
														value={bloco.codigo}
														onChange={e => { bloco.codigo = e.target.value; updateCodelist(bloco, index) }}
													/>
												</TableCell>
												<TableCell>
													<TextInput
														size="sm"
														style={{ fontSize: '0.65rem' }}
														value={bloco.aplicabilidade}
														onChange={e => { bloco.aplicabilidade = e.target.value; updateCodelist(bloco, index) }}
													/>
												</TableCell>
												<TableCell>
													<MisuseOutline16 style={{ fill: 'red' }} onClick={(e) => removerBloco(e, index)} />
												</TableCell>
											</TableRow>
										))}
									</TableBody>
								</Table>
							</TableContainer>
						)}
					</DataTable>

					<div style={{ display: 'flex' }}>
						<Button
							kind="secondary"
							style={{ flexGrow: 1, padding: 0, justifyContent: 'center' }} onClick={handleCancel}
						>
							Cancel
						</Button>
						<Button style={{ flexGrow: 1, padding: 0, justifyContent: 'center' }} onClick={handleSave}>
							Save
						</Button>
					</div>
				</Form>
			</div>
		)
	}

 
	
  ```
</details>



<details>
  <summary>Controller para busca dos manuais</summary>


	Tela para poder fazer a busca dos manuais

  
  ```java
	@CrossOrigin("http://localhost:3000")
	@Controller
	@RequestMapping("/api/manual")
	@Api(value = "Manual")
	public class ManualController {

		@Autowired
		ManualRepository repository;

		@GetMapping
		public ResponseEntity<List<Manual>> getAllManuals() {
			try {
				List<Manual> manuals = repository.findAll();

				if (manuals.isEmpty()) {
					return new ResponseEntity<>(HttpStatus.NO_CONTENT);
				}

				return new ResponseEntity<>(manuals, HttpStatus.OK);
			} catch (Exception e) {
				return new ResponseEntity<>(null, HttpStatus.INTERNAL_SERVER_ERROR);
			}
		}
	}

  ```
</details>

<div align="center">

**Hard Skills**
|**Tecnologia/Metodologia**|**Classificação**        |
|--------------------------|-----------------------|
|HTML                      |Sei fazer com Autonomia|
|CSS                       |Sei fazer com Autonomia|
|JavaScript                |Sei fazer com Ajuda    |
|Git                       |Sei fazer com Ajuda    |
|GitHub                    |Sei fazer com Ajuda    |
|Java                      |Sei fazer com Ajuda    |
|Carbon                    |Sei fazer com Ajuda    |
|Postgre                   |Sei fazer com Autonomia|



**Soft Skills**
|**Habilidade**     |**Descrição**        |
|-------------------|---------------------|
|Organização|Capacidade de planejar e gerenciar tarefas de forma eficiente.|
|Trabalho em Equipe|Habilidade de colaborar e comunicar efetivamente com outros membros da equipe para alcançar objetivos comuns.|
|Capacidade de planejamento| Habilidade de elaborar planos detalhados para alcançar metas específicas. Isso envolve a habilidade de priorizar tarefas, estabelecer cronogramas realistas e ajustar planos conforme necessário para garantir o sucesso do projeto.|
|Atenção para ouvir|Capacidade de ouvir atentamente as ideias, preocupações e feedback de colegas, clientes e outras partes interessadas, demonstrando empatia e compreensão.|

</div>



