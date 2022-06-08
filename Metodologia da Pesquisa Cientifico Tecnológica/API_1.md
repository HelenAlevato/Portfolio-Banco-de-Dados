## Meu Primeiro API  📚

#### Em 2020-1 (API 1)
Trabalhei no projeto da API do primeiro semestre. O master era um integrante do sexto semestre. O professor Fabiano S. foi o orientador. [GitHub do projeto.](https://github.com/Projeto-Integrador-BD)<br> 
- **Nome do Grupo:** ivy-projeto-bd
- **Nome do Software:**  Ivy
- **Visão do Produto:** Gerenciamento de produtividade pessoal para o dia a dia.
     
 - **Objetivo do Produto:** 
	  - Assistente vistual de voz
  
- **Problema (Desafio):** 

	- Fazer uma Assistente Virtual para auxiliar nas atividades do dia.

- **Proposta:**

	- Após reunião do grupo decidimos fazer uma assistente de voz para auxiliar em algumas atividades do cotidiano. Elas foram:
	
	- Calcule: A Ivy fará cálculos simples de adição, subtração, multiplicação e divisão. O usuário solicitará o cálculo de dois números e a assistente vai dar o resultado do cálculo.

	- Cronometro de atenção: Essa aplicação irá auxiliar o usuário a manter o foco em tarefas de seu trabalho ou estudos evitando distrações ao acessar sites e redes sociais.
	
	- Gerar senha: Gerar senhas com base nos critérios do usuário e opções disponibilizadas pela ferramenta. O usuário irá conversar com a Ivy e por meio de perguntas escolherá as opções disponíveis para a geração de senha.
	
	- Informação de clima: Previsão atual do tempo, verificando se vai fazer sol ou chuva.
	
	- Pesquisa: pesquisar informações no Google.

#### Vídeos explicativos do projeto feitos por mim 📺
- [Apresentação da ideia inicial do projeto](https://www.youtube.com/watch?v=mC4Ij5v4oQo)
- [Apresentação final do projeto](https://www.youtube.com/watch?v=nHQFg2epm9o)

#### Tecnologias Utilizadas 🛠
Reconhecimento de Voz utilizando a API do Google, API do sexto semestre, Visual Studio Code.

## Contribuições Pessoais 👩
Nesse trabalho todos ficamos como desenvolvedores, dividindo as tarefas entre as funcionalidades. Além disso eu fiquei responsável pela criação do nome, identidade visual do trabalho, vídeos de apresentação e Readme.
<br/>

**Desenvolvimento:**  

<details>
  <summary>Funcionalidade de captura de voz: Importei a biblioteca para que o reconhecimento fosse possível no trabalho.</summary>
  
  ```python
    # Necessário instalar o pyAudio: 
	# pip install pyaudio
	# depois instala o speech_recognition: 
	# pip install SpeechRecognition
	import speech_recognition as sr

	# cria uma variavel para reconhecimento do audio
	reconhecedor = sr.Recognizer()

	with sr.Microphone() as source:
	    # passar o que o programa ouviu para a variavel audio
	    audio = reconhecedor.listen(source)

	    # imprime o audio e passa para o algoritmo de reconhecimento escolhido
	    # no caso, a google
	    print(reconhecedor.recognize_google(audio, language="pt-BR"))

	print("FIM DO PROGRAMA") 
  ```
</details>

<details>
  <summary>Funcionalidade de Gerar Senha: Fiz com que a assistente de voz gerasse uma senha aleatória, baseado em alguns critérios.</summary>
  
  ```python
	def gerar_senha():
	lista_simbolos= ["!", "@", "#", "$", "%", "&", "*"]
	letras = ["a", "b", "c", "d","e","f","g","i","j","k","l","m","n","o","p","q","r","s","t","u","v","w","x","y","z"]
	gerar_palavras = True
	gerar_numeros = True
	gerar_0_9 = True
	gerar_simbolos = True
	gerar_abc = True
	qtde_abc = 5
	gerar_maiusculo = True
	senha = ""
	if gerar_simbolos:
	valor = random.randint(0, len(lista_simbolos))
	senha += lista_simbolos[valor]
	if gerar_numeros:
	if gerar_0_9:
	valor = random.randint(0, 9)
	senha += str(valor)
	if gerar_abc:
	for i in range(qtde_abc):
	valor = random.randint(0, len(letras))
	senha += letras[valor]
	print ("sua senha é: " + senha)
	return senha
  ```
</details>


#### Hard Skills Efetivamente Desenvolvidas
* Python

#### Soft Skills Efetivamente Desenvolvidas
* Autonomia
* Lógica de programação
* Flexibilidade e adaptabilidade
* Suportar críticas
* Atitude positiva
