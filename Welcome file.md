
# Guia do Projeto: [AUTOMAÇÕES COM N8N]


**Disciplina:** [Sistemas de Informação]
**Alunos:** Victor Alves e Matheus Dallacort 

---

## 1. Introdução

Seja bem-vindo ao projeto de automação com n8n e WhatsApp! No mundo digital de hoje, a comunicação instantânea é fundamental. Ferramentas como o WhatsApp não são apenas para conversas pessoais, mas também se tornaram canais poderosos para negócios, suporte ao cliente e otimização de processos.

Neste projeto, vamos explorar como podemos programar e automatizar interações no WhatsApp. Para isso, utilizaremos duas ferramentas principais: o **n8n**, uma plataforma *low-code* de automação de fluxos de trabalho que permite conectar diferentes sistemas e APIs de forma visual e intuitiva, e o **WAHA (WhatsApp HTTP API)**, uma solução que atua como uma ponte, permitindo que nossos sistemas enviem e recebam mensagens do WhatsApp.

O objetivo central é construir uma automação funcional que escute por novas mensagens recebidas em um número de WhatsApp e execute uma ação específica como resposta, criando, na prática, um bot de conversação simples.

Este guia irá conduzi-lo passo a passo, desde a configuração do ambiente até a criação do seu primeiro fluxo de automação. Ao final, você terá um conhecimento prático sobre integração de APIs e automação de processos, habilidades muito valorizadas no mercado de tecnologia.

## 2. Etapas do Projeto (Guia Prático)

Nesta seção, vamos detalhar todos os passos necessários para construir nossa automação, desde a configuração inicial até o fluxo final funcionando.

### Etapa 1: Configuração do Ambiente de Desenvolvimento

Para garantir que nosso projeto funcione de forma isolada e consistente em qualquer máquina, utilizaremos o Docker. Ele nos permitirá executar o n8n e o WAHA em "contêineres", que são como mini-máquinas virtuais leves e pré-configuradas.

#### 1.1. Instalação do Docker Desktop no Windows

O Docker Desktop é a maneira mais fácil de usar o Docker em um ambiente Windows.

**Pré-requisitos:**
* A virtualização de hardware deve estar **ativada na BIOS/UEFI** do seu computador.`Intel VT-x` ou `AMD-V`.

**1.2 Passos para a Instalação:**

1.2.1.  **Baixar o Instalador:**
    * Acesse o site oficial do Docker: **https://www.docker.com**    
    * * Clique no botão para baixar a versão para Windows.

1.2.2.  **Executar a Instalação:**
    * Encontre o arquivo `Docker Desktop Installer.exe` que você baixou e execute-o com privilégios de administrador (clique com o botão direito -> "Executar como administrador").
    * Na tela de configuração, certifique-se de que a opção **"Install required Windows components for WSL 2"** esteja marcada. Esta é a configuração recomendada.
    * Siga as instruções na tela. Ao final, o Docker solicitará que você **reinicie o computador**. Faça isso para que todas as configurações sejam aplicadas.

1.2.3.  **Verificar a Instalação:**
    * Após reiniciar, abra o Docker Desktop pelo menu Iniciar. Ele pode levar um minuto para iniciar o serviço.
    * Abra um terminal (PowerShell ou CMD) e digite o seguinte comando para confirmar que o Docker foi instalado:
        ```sh
        docker --version
        ```
        Você deverá ver uma resposta como `Docker version 28.3.2, build 578ccf6`.

## 3. Mãos à Obra: Do Repositório à Execução

Agora que temos o Docker instalado e pronto, é hora de dar vida ao nosso ambiente de automação. O "coração" do nosso projeto é o arquivo `docker-compose.yml`, que contém todas as instruções para o Docker criar e conectar os serviços do n8n e do WAHA.

Para garantir que todos usem a mesma configuração, este arquivo está hospedado em um repositório no GitHub. Vamos baixá-lo e iniciar nosso projeto.

**Passos para a Configuração:**

3.1.  **Acesse o Repositório do Projeto:**
    * Abra o seu navegador e vá para o link do nosso repositório oficial no GitHub:
        * **https://github.com/alvesvsolda/n8n-waha/blob/main/docker-compose.yml**

3.2.  **Baixe o Arquivo `docker-compose.yml`:**
    * No repositório, localize o arquivo chamado `docker-compose.yml`.
    * Clique nele para abri-lo.
    * Clique no botão **"Download raw file"** para baixar o arquivo.


3.3.  **Prepare a Pasta do Projeto:**
    * Crie uma pasta em seu computador onde o projeto irá residir (por exemplo, em `Documentos/n8n-waha`).
    * Mova o arquivo `docker-compose.yml` que você acabou de baixar para dentro desta nova pasta.

3.4.  **Inicie os Serviços com Docker Compose:**
    * Abra um terminal (PowerShell ou CMD).
    * Navegue até a pasta do seu projeto usando o comando `cd`. Por exemplo:
        ```sh
        PS C:\Users\Alves> cd .\Documents\n8n-waha\
        ```
    * Execute o seguinte comando. Ele irá ler o arquivo, baixar as imagens necessárias e iniciar os contêineres em segundo plano:
        ```sh
        docker-compose up -d
        ```

5.  **Verifique se Tudo Está Rodando:**
    * Para confirmar que os contêineres estão ativos, abra o docker e selecione "Containers"
    * Se tudo der certo você verá "n8nwahalocal", apertando na setinha para baixo, você vai ver todos os serviços rodando no container.

## 4. Configurando o Ambiente: 

4.1.  **Nos containers vamos iniciar a configuração do WAHA!**

**Passos para a Configuração:**

 * Em: "waha-1" vamos apertar no link [3000:3000](http://localhost:3000).
 * Após isso (na tela do Swagger) vamos apertar em "[Dashboard](http://localhost:3000/dashboard)".
 * Vamos iniciar o serviço e escanear o QR Code.
 
4.2.  **Configurando o N8N!**

**Passos para a Configuração:**

 * Em: "n8n-1" vamos apertar no link [5678:5678](http://localhost:5678).
 * Preencha o cadastro com:
 - [x] Email (Para receber uma Key).
 - [x] Nome.
 - [x] Sobrenome.
 - [x] Senha.

4.3.  **IMPORTANTE !**

> I´m not using n8n for work

4.4 **Vamos adicionar o node para fazer a conexão entre o N8N e o WAHA**

	No campo vamos digitar: n8n-nodes-waha

## 5. Workflow

Vamos iniciar o nosso workflow com um  Trigger:

## On Webhook call.

> **HTTP Method: Post**
>  **Path: webhook**


Vamos voltar no Waha e configurar o Webhook

> **Configurações**
> Cola URL teste
> **Events**
> message

> **Update**

Teste seu Webhook

5.1 **Agora vamos adicionar um filtro com o widget "Set"**
nele, vamos colocar os seguintes campos:
# **session:** `session(body)`
# **chatId:** `from(payload)`
# **pushName:** `notifyName(media)`
# **payload_id:** `payload(id)`
# **event:** `event(body)`
# **message:** `body(payload)`
# **fromMe:** `fromMe(payload)`
	
5.2 **Com isso temos nossos dados filtrados, após isso vamos adicionar um campo "Switch".**	

Nele vamos comprar se o "event" (evento ao qual filtramos) é igual a uma mensagem "message".
E vamos testar.

5.3 **Agora vamos começar a mágica, adicionando um Agente IA.**	
Nele nós vamos passar as instruções para dizer como vamos continuar o fluxo.

  
# **Source for prompt:** `Define Below`

# **Prompt (User Message):** `Parâmetro: message`

# **Add Option:** `System Message: (Aqui vai o prompt (instrução)`



5.4 **Agora vamos definir a LLM que vamos usar: **

>Em Chat Model, vamos selecionar o desejado.
Após escolhido, vamos criar as credenciais.	

Após criado e salvo, vamos escolher o modelo, e definir um sample temperature (
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5MTEzNDEyMTMsLTM5MTQ0MjgzMSwtMz
Y2ODg2ODUwLC0xNjA2NjcyMjA1LDkyMDQxOTcwNiwtMTc0NzMy
MDUwMywtMTc2NTYxNDAyNV19
-->