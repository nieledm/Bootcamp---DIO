## Introducao ao Git/GitHub

# Linhas de comando

Windows		Unix
- cd			- cd			(navegar entre as pastas)
- dir			- is			(listas de diretorios)
- mkdir		- mkdir		(criar pasta)
- del/rmdir		- rm-rf		(del - deleta arquivos/ rmdir - deleta diretorio)	
- cd..		- cd..		(retrocede uma etapa)
- cls			- clear ou ctrl+l	(limpar o terminal)
- mv 						(move um arquivo de um lugar para outro)

obs: Usar o TAB para autocompletar

- echo (printa no terminal uma frase)
	ex: echo hello > hello.txt
	Primeiro verifica se tem esse arquivo "hello", caso nao tenha ele vai criar
- rmdir. Ex: rmdir nome_do_diretorio_(pasta) /s /q
- mv. Ex: mv nome_do_arquivo_e_sua_extensao ./nome_da_pasta/

# Como o Git funciona por baixo dos panos

- sha1 - algoritimo de incriptacao
	openssl sha1 ...
	obs1: Arquivos com os mesmos carcteres irao gerar sempre o mesmo codigo de incriptacao
	obs2: Pode ser usado como verificador de arquivo

# Objetos internos do Git (Blobs, Trees, Commits)

- Blobs: Funcao: git hash --- Passando diretamente pelo Git
		blob 9\0 ... 
		openssl sha1 --- Gera o mesmo codigo

- Tree: Armazena os blobs --- tree \0


				TREE
				/ | \
			     /  |  \
			    /   |   \
			   /    |    \
	          READNE PAKEFILE LIB
			 /      |      \
		    BLOB    BLOB    TREE
					    |
				    simplegit.rb
					    |
					  BLOB

- Commit: Aponta para:
		- Tree
		- Parente (commit)
		- Autor
		- Mensagem
		- Timestamp
	O sha1 desse commit e o hash de toda essa informacao
	Se olha o historico tem como saber se alguem alterou o arquivo
	Consegue-se ver todo o historico de commits = linha do tempo

# Chaves SSH e Tokens (conexao Git Bash / GitHub)

- Chave SSH: Forma de se estabelecer uma conexao segura e incriptada entre duas maquinas
	No inicio iremos usar essa chave para cadastrar nossa maquina no GitHub e nunca mais precisaremos de senha para enviar ou receber arquivos do GitHub

	Caminho para a chave:
	- Clicar na imagem do seu perfio do GitHub
	- Settings
	- A esquerda: SSH and GPG Keys

	Como gerar chave SSH?
	- No Git Bash:
		ssh-keygen -t ed25519 -C seu_endereco_de_email --- Enter
		Colocar uma senha --- Enter

	- Va ate a pasta informada pelo Git Bash de onde esta a sua chave
		cd /c/users/nome_do_computador/.ssh/ --- Enter

	- Para ver o conteudo de uma das chaves:
		cat id_chave.pub -- obs: chave = numero dado pelo Git Bash
	- Copie a chave mostrada e cole no GitHub

	- Iniciar o ssh agent no Git Bash
		eval$ (ssh-agent -s) --- enter
		ssh-add chave_privada --- enter
		senha ---enter

	- Como clonar um repositorio GitHub:
		- Ir na caixa verde (CODE) do repositori no GitHub e pegar o clone SSH
		- No Git Bash va ate sua pasta de interesse 
		- Colar o SSH no Git Bash
			git clone colar_a_chave_SSH_clonada --- Enter
			yes --- Enter

- Token de acesso pessoal
	Se assemelha a colocar Nickname e senha
	Gerar um token no GitHub e depois armazenar para usar quando preciso

	- Va ao GitHub
	- Clicar na sua imagem de perfil
	- Setting
	- A esquerda: Developer settings
	- Personal access tokens
	- Generate new token
		obs: Marcar a opcao REPO (Permite mexer nas coisas padrao do Git no terminal)
	- Generate token
	- COPIAR O TOKEN E SALVAR EM LUGAR SEGURO
	- Retornar ao repositorio privado
	- Code
	- Clone: protocolo HTTPS (copiar o link)
	- Ir ao terminal Git Bash
		Em pasta reservada
		git clone colar_a_URLS --- Enter
		colar_o_token --- Enter

# Alguns comandos do Git

- git init: Iniciar repositorio e criar repositorio
- git add: Mover arquivo para commit
	obs1: Se usar "git add *" tudo dentro da pasta sera modificado
	obs2: Usar flag -m para add comentario ao commit
		git add * -m "comentario"
- git commit: Criar commit
- git status: Mostrar o status dos arquivos

Configurar o Git oara fazer commit:
	obs: Isso deve ser feito na primeira vez que usar o Git
	git config --global user.email endereco_de_emai --- enter
	git config --global user.name nome --- enter

obs: O repositorio local tem que ser formado por commits. Se voce nao "commitar" o arquivo voce nao consegue jogar o repositorio local para o repositorio remoto


# Trabalhando com GitHub

- Para ver suas configuracoes no Git:
	git config --list
- Se precisar modificar as configuracoes:
	git config --global --unset nome_da_propriedade_que_deseja_modificar --- Enter
	git config --global nome_da_propriedade_que_deseja_modificar novo_nome

- git remote add origin link_do_GitHub_do_repositorio
	Move o repositorio local para a nuvem
- git remote -v
	lista de repositorios cadastrados
- git push origen master
	Emperra o repositorio local para o remoto