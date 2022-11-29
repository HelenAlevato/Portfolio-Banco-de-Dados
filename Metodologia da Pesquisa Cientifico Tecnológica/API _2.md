## Meu Segundo API  📚

#### Em 2020-2 (API 2)
Trabalhei no projeto da API com o Parceiro TecSus. [GitHub do projeto.](https://github.com/HelenAlevato/PI-GRUPO-6)<br> 
- **Nome do Grupo:** GRUPO-6
- **Nome do Software:**  G6
- **Visão do Produto:** Sistema de digitação e edição de contas.
     
 - **Objetivo do Produto:** 
	- Sistema de digitação e edição de contas para mais agilidade e rapidez no trabalho.
  
- **Problema (Desafio):** 

	- O problema era o grande volume de contas que os digitadores precisavam digitar manualmente no sistema.

- **Proposta:**

	- A proposta era fazer um sistema que melhorasse a rotina de digitação dos funcionários. 
  -  Filtrar e selecionar o tipo de conta desejada referente a um cliente específico, pois o digitador necessita verificar qual tipo de conta será editada e qual mês e ano de referência. Objetivo principal para auxiliar na alteração, visualização e separação dos tipos de contas ajudando na correção de possíveis erros.
  - Gerenciar cada tipo de conta em um campo específico, que seja no modelo da empresa escolhida, pois a dificuldade está na forma que o digitador coloca os dados no sistema, cada conta com seus campos específicos ficaria mais intuitivo e prático para que o resultado final tenha mais agilidade. Para poder alterar e acessar os campos necessários referentes a cada conta.

  <br>

#### Tecnologias Utilizadas
Eclipse
Java Fx 
MYSQL 
JAVA versão 11

## Contribuições Pessoais
Nesse trabalho fiquei como desenvolvedora, responsável também por algumas apresentação, readme e gravação de vídeos explicativos do sistema.


**Desenvolvimento:**  

Telas feitas para o sistema
  - Cadastro Cliente: Tela para cadastrar os usuários que contratarem o sistema da empresa;
  - Cadastro Imovel: Dados cadastrais do imóvel ou imoveis do usuário;
  - Cadastro Usuário: Tela para cadastrar o funcionário que irá mexer no sistema;
  - Conta Água: Tela para facilitar na digitação dos campos das contas de água;
  - Conta Gás: Tela para facilitar na digitação dos campos das contas de gás;
  - Conta Luz: Tela para facilitar na digitação dos campos das contas de luz;
  - Menu: barra de navegação para acessar as outras telas de forma mais rápida.
  
Funcionalidades 
- Organização das telas e Adição da funcionalidade limpar
- Inclusão das mascaras
- Inserção de usuário e cliente no Banco pela tela
- Busca do cliente na conta de luz
- Movimentação dos documentos para /doc
- Adição da tela de Cadastro de Imóvel
- Busca do imovel/cliente para o cadastro das contas
- Tela Busca
- Adição do Tooltip
- Ícone da aplicação
- Adição do JAR

Código de exmplo na construção das telas

<details>
  <summary>Exemplo do desenvolvimento de uma das telas, no caso Conta de Água</summary>
	
	Na tela de conta, nesse caso a de água foi pega as informações principais das contas de água e feito um formulario 
	para que o usuário que precisar digitar a conta consiga fazer isso de forma fácil e rápida.
  
  ```java
	package application.controllers;

	import java.net.URL;
	import java.security.NoSuchAlgorithmException;
	import java.sql.Date;
	import java.util.Optional;
	import java.util.ResourceBundle;

	import application.models.Cliente;
	import application.models.ContaAgua;
	import application.models.Imovel;
	import application.models.dao.ClienteSQL;
	import application.models.dao.ContaAguaSQL;
	import application.models.dao.ImovelSQL;
	import application.util.TextFieldFormatter;
	import application.util.ValidationFields;
	import javafx.beans.value.ChangeListener;
	import javafx.beans.value.ObservableValue;
	import javafx.event.ActionEvent;
	import javafx.fxml.FXML;
	import javafx.fxml.Initializable;
	import javafx.scene.control.Alert;
	import javafx.scene.control.Button;
	import javafx.scene.control.ButtonType;
	import javafx.scene.control.DatePicker;
	import javafx.scene.control.TextField;
	import javafx.scene.control.Alert.AlertType;
	import javafx.scene.layout.BorderPane;

	public class ContaAguaController implements Initializable {

		@FXML
		private TextField txtEsgoto;

		@FXML
		private TextField txtNomeTitular;

		@FXML
		private TextField txtTipoFaturamento;

		@FXML
		private TextField txtRgi;

		@FXML
		private DatePicker txtDataVencimento;

		@FXML
		private TextField txtNumero;

		@FXML
		private TextField txtValorLeituraAtual;

		@FXML
		private TextField txtComplemento;

		@FXML
		private BorderPane btnContaAgua;

		@FXML
		private TextField txtAgua;

		@FXML
		private TextField txtCidade;

		@FXML
		private TextField txtTotalPagar;

		@FXML
		private Button btnLimpar;

		@FXML
		private TextField txtValorLeituraAnterior;

		@FXML
		private TextField txtConsumo;

		@FXML
		private DatePicker txtDataLeituraAtual;

		@FXML
		private TextField txtRua;

		@FXML
		private TextField txtTipoLigacao;

		@FXML
		private TextField txtCodigoCliente;

		@FXML
		private TextField txtUf;

		@FXML
		private TextField txtPeriodoConsumo;

		@FXML
		private TextField txtCep;

		@FXML
		private TextField txtHidrometro;

		@FXML
		private DatePicker txtDataLeituraAnterior;

		@FXML
		private TextField txtBairro;

		private Imovel imovel;
		private Cliente cliente;

		void dadosIniciais(String nomeTitular, Imovel imovel) {
			txtNomeTitular.setText(nomeTitular);
			this.imovel = imovel;

			txtRgi.setText(String.valueOf(this.imovel.getIdentificacaoImovel()));
			txtUf.setText(this.imovel.getUfImovel());
			txtCidade.setText(this.imovel.getCidadeImovel());
			txtBairro.setText(this.imovel.getBairroImovel());
			txtRua.setText(this.imovel.getRuaImovel());
			txtNumero.setText(this.imovel.getNumImovel());
			txtComplemento.setText(this.imovel.getComplementoImovel());
			txtCep.setText(this.imovel.getCepImovel());
		}

		@FXML
		private void txtCepKeyReleased() {
			TextFieldFormatter tff = new TextFieldFormatter();
			tff.setMask("#####-###");
			tff.setCaracteresValidos("0123456789");
			tff.setTf(txtCep);
			tff.formatter();
		}

		@FXML
		void clickLimpar(ActionEvent event) {
			txtRgi.setText("");
			txtNomeTitular.setText("");
			txtUf.setText("");
			txtCidade.setText("");
			txtBairro.setText("");
			txtRua.setText("");
			txtNumero.setText("");
			txtComplemento.setText("");
			txtCep.setText("");
			txtCodigoCliente.setText("");
			txtTipoLigacao.setText("");
			txtHidrometro.setText("");
			txtTipoFaturamento.setText("");
			txtPeriodoConsumo.setText("");
			txtAgua.setText("");
			txtEsgoto.setText("");
			txtConsumo.setText("");
			txtValorLeituraAtual.setText("");
			txtValorLeituraAnterior.setText("");
			txtDataLeituraAtual.setValue(null);
			txtDataLeituraAnterior.setValue(null);
			txtDataVencimento.setValue(null);
			txtTotalPagar.setText("");
		}

		@FXML
		void clickEditar(ActionEvent event) {

		}

		@FXML
		void clickCadastrar(ActionEvent event) throws NoSuchAlgorithmException {
			Alert alert = new Alert(AlertType.CONFIRMATION);
			alert.setTitle("Caixa de Confirmação");
	//		alert.setHeaderText("Caixa de diálogo de confirmação");
			alert.setContentText("Deseja realmente cadastrar uma nova conta de Água");

			Optional<ButtonType> result = alert.showAndWait();
			if (result.get() == ButtonType.OK) {

				// Verifica se há campos obrigatórios não preenchidos
				boolean camposPreenchidos = ValidationFields.checkEmptyFields(txtRgi, txtCodigoCliente, txtTipoLigacao,
						txtHidrometro, txtTipoFaturamento, txtPeriodoConsumo, txtAgua, txtEsgoto, txtConsumo,
						txtValorLeituraAtual, txtValorLeituraAnterior, txtDataLeituraAtual, txtDataLeituraAnterior,
						txtDataVencimento, txtTotalPagar);

				if (camposPreenchidos) {
					int rgi = Integer.parseInt(txtRgi.getText());
					int codigoCliente = Integer.parseInt(txtCodigoCliente.getText());
					String tipoLigacao = txtTipoLigacao.getText();
					String hidrometro = txtHidrometro.getText();
					String tipoFaturamento = txtTipoFaturamento.getText();
					String periodoConsumo = txtPeriodoConsumo.getText();
					String agua = txtAgua.getText();
					String esgoto = txtEsgoto.getText();
					String consumo = txtConsumo.getText();
					float valorLeituraAtual = Float.parseFloat(txtValorLeituraAtual.getText());
					float valorLeituraAnterior = Float.parseFloat(txtValorLeituraAnterior.getText());
					Date dataLeituraAtual = Date.valueOf(txtDataLeituraAtual.getValue());
					Date dataLeituraAnterior = Date.valueOf(txtDataLeituraAnterior.getValue());
					Date dataVencimento = Date.valueOf(txtDataVencimento.getValue());
					float totalPagar = Float.parseFloat(txtTotalPagar.getText());

					ContaAgua contaAgua = new ContaAgua(0, cliente.getId_cli(), rgi, codigoCliente, tipoLigacao, hidrometro, tipoFaturamento,
							periodoConsumo, agua, esgoto, consumo, valorLeituraAtual, valorLeituraAnterior,
							dataLeituraAtual, dataLeituraAnterior, dataVencimento, totalPagar);
					ContaAguaSQL contaAguaSQL = new ContaAguaSQL();
					contaAguaSQL.create(contaAgua);
				}
			} else {

			}
		}

		@FXML
		void clickBuscarImovel(ActionEvent event) {
			buscarImovel();
		}

		public void buscarImovel() {
			System.out.println("nr de identificação: " + txtRgi.getText() + "\n");
			if (!"".equals(txtRgi.getText())) {
				ImovelSQL imovelSQL = new ImovelSQL();
				ClienteSQL clienteSQL = new ClienteSQL();

				int codIdentificacao = Integer.parseInt(txtRgi.getText());
				imovel = imovelSQL.buscarImovelPeloCodIdentificacao(codIdentificacao);
				cliente = clienteSQL.buscarClientePorId(imovel.getIdCliente());
				txtNomeTitular.setText(cliente.getNome_cli());
				txtCep.setText(imovel.getCepImovel());
				txtUf.setText(imovel.getUfImovel());
				txtCidade.setText(imovel.getCidadeImovel());
				txtComplemento.setText(imovel.getComplementoImovel());
				txtBairro.setText(imovel.getBairroImovel());
				txtRua.setText(imovel.ruaImovel);
				txtNumero.setText(String.valueOf(imovel.getNumImovel()));
			}
		}

		@Override
		public void initialize(URL location, ResourceBundle resources) {
			txtRgi.focusedProperty().addListener(new ChangeListener<Boolean>() {
				@Override
				public void changed(ObservableValue<? extends Boolean> arg0, Boolean oldPropertyValue,
						Boolean newPropertyValue) {
					if (newPropertyValue) {
						System.out.println("clicou no campo");
					} else {
						buscarImovel();
					}
				}
			});
		}
	}
  ```
</details>

<details>
  <summary>Menu Controller</summary>


	No menu controler foi centralizado um menu de cabeçalho, nele temos uma barra de pesquisa e vários botões para que o usuário 
	consiga já identificar qual caminho ele irá tomar, esses potões redirecionam para as telas que são:
		- Cadastro usuário
		- Cadastro cliente
		- Conta Luz
		- Conta Gás
		- Conta Água
		- Cadastro Imovel

  
  ```java
	package application.controllers;

	import java.io.IOException;
	import java.net.URL;
	import java.util.ResourceBundle;

	import javafx.application.Platform;
	import javafx.event.ActionEvent;
	import javafx.fxml.FXML;
	import javafx.fxml.FXMLLoader;
	import javafx.fxml.Initializable;
	import javafx.scene.control.Button;
	import javafx.scene.layout.AnchorPane;
	import javafx.scene.layout.BorderPane;
	import javafx.scene.layout.HBox;

	public class MenuController implements Initializable {

		private BorderPane rootLayout;

		@FXML
		private Button btnCadastroUsuario;

		@FXML
		private Button btnCadastroCliente;

		@FXML
		private Button btnContaLuz;

		@FXML
		private Button btnContaAgua;

		@FXML
		private Button btnContaGas;

		@FXML
		private Button btnCadastroImovel;

		@FXML
		private Button btnBuscar;

		@FXML
		public HBox cabecalho;

		public boolean mostrarCabecalho;

		@FXML
		private void clickCadastroUsuario(ActionEvent evento) throws IOException {
			rootLayout = (BorderPane) btnCadastroCliente.getScene().getRoot();
			BorderPane menuLayout = (BorderPane) rootLayout.getCenter();

			FXMLLoader loader = new FXMLLoader();
			loader.setLocation(MenuController.class.getResource("/application/views/CadastroUsuario.fxml"));
			AnchorPane cadastroUsuario = (AnchorPane) loader.load();

			menuLayout.setCenter(cadastroUsuario);
		}

		@FXML
		private void clickCadastroCliente(ActionEvent evento) throws IOException {
			rootLayout = (BorderPane) btnCadastroCliente.getScene().getRoot();
			BorderPane menuLayout = (BorderPane) rootLayout.getCenter();

			FXMLLoader loader = new FXMLLoader();
			loader.setLocation(MenuController.class.getResource("/application/views/CadastroCliente.fxml"));
			AnchorPane cadastroCliente = (AnchorPane) loader.load();

			menuLayout.setCenter(cadastroCliente);
		}

		@FXML
		private void clickContaLuz(ActionEvent evento) throws IOException {
			rootLayout = (BorderPane) btnCadastroCliente.getScene().getRoot();
			BorderPane menuLayout = (BorderPane) rootLayout.getCenter();

			FXMLLoader loader = new FXMLLoader();
			loader.setLocation(MenuController.class.getResource("/application/views/ContaLuz.fxml"));
			BorderPane contaLuz = loader.load();

			menuLayout.setCenter(contaLuz);
		}

		@FXML
		private void clickContaAgua(ActionEvent evento) throws IOException {
			rootLayout = (BorderPane) btnCadastroCliente.getScene().getRoot();
			BorderPane menuLayout = (BorderPane) rootLayout.getCenter();

			FXMLLoader loader = new FXMLLoader();
			loader.setLocation(MenuController.class.getResource("/application/views/ContaAgua.fxml"));
			BorderPane contaAgua = loader.load();

			menuLayout.setCenter(contaAgua);
		}

		@FXML
		private void clickContaGas(ActionEvent evento) throws IOException {
			rootLayout = (BorderPane) btnCadastroCliente.getScene().getRoot();
			BorderPane menuLayout = (BorderPane) rootLayout.getCenter();

			FXMLLoader loader = new FXMLLoader();
			loader.setLocation(MenuController.class.getResource("/application/views/ContaGas.fxml"));
			BorderPane contaGas = loader.load();

			menuLayout.setCenter(contaGas);

		}

		@FXML
		private void clickCadastroImovel(ActionEvent evento) throws IOException {
			rootLayout = (BorderPane) btnCadastroCliente.getScene().getRoot();
			BorderPane menuLayout = (BorderPane) rootLayout.getCenter();

			FXMLLoader loader = new FXMLLoader();
			loader.setLocation(MenuController.class.getResource("/application/views/CadastroImovel.fxml"));
			BorderPane cadastroImovel = (BorderPane) loader.load();

			menuLayout.setCenter(cadastroImovel);
		}

		@FXML
		private void clickBuscar(ActionEvent evento) throws IOException {
			rootLayout = (BorderPane) btnCadastroCliente.getScene().getRoot();
			BorderPane menuLayout = (BorderPane) rootLayout.getCenter();

			FXMLLoader loader = new FXMLLoader();
			loader.setLocation(MenuController.class.getResource("/application/views/Busca.fxml"));
		BorderPane buscar = (BorderPane) loader.load();

		menuLayout.setCenter(buscar);

		}

		@Override
		public void initialize(URL location, ResourceBundle resources) {
			Platform.runLater(() -> {
				cabecalho.setVisible(mostrarCabecalho);
		    });
		}

		public void setMostrarCabecalho(boolean mostrarCabecalho) {
			this.mostrarCabecalho = mostrarCabecalho;
		}

	}
  ```
</details>




#### Hard Skills Efetivamente Desenvolvidas
Eclipse
Java Fx 
MYSQL 
JAVA versão 11

#### Soft Skills Efetivamente Desenvolvidas
Autonomia<br>


