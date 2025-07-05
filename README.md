# n8n Automated Workflow Backup 🚀

Este repositório contém um fluxo n8n para realizar **backups automatizados** dos seus fluxos n8n para um repositório GitHub.

## 🌟 Visão Geral

Já pensou em perder todos os seus fluxos n8n por acidente? Com este projeto, isso não será mais uma preocupação! Ele permite que você mantenha um **histórico de todas as suas alterações** nos fluxos n8n e tenha um ponto de recuperação seguro em caso de qualquer imprevisto. O fluxo n8n exporta automaticamente seus fluxos e os envia para um repositório GitHub de sua escolha, garantindo que você sempre tenha uma cópia de segurança.

## ✨ Funcionalidades

* **Backup Automatizado**: Garante que todos os seus fluxos n8n sejam copiados regularmente.
* **Versionamento de Fluxos**: Utilize o poder do Git para acompanhar cada alteração nos seus fluxos.
* **Restauração Simples**: Recupere seus fluxos facilmente a partir do GitHub, se precisar.

---

## 🛠️ Pré-requisitos

Para começar, você precisará do seguinte:

* Uma instância **n8n** em execução.
* Uma conta **GitHub**.

---

## 🚀 Configuração Passo a Passo

Siga este guia para configurar seu backup automatizado:

### 1. Configurar Credenciais GitHub no n8n

1.  No n8n, navegue até "**Credenciais**" e clique em "**Adicionar Credencial**".
2.  Pesquise por "**GitHub OAuth**" e selecione-o.
3.  **Copie** a "**URL de Autenticação**" que o n8n fornece.
4.  No GitHub, vá para "**Settings**" > "**Developer settings**" > "**OAuth Apps**" e clique em "**New OAuth App**".
5.  Preencha os campos com os seguintes dados:
    * **Application name:** `n8n` (ou o nome que preferir)
    * **Homepage URL:** A URL da sua instância n8n (ex: `https://seu-n8n-instance.com`)
    * **Authorization callback URL:** **Cole** a "URL de Autenticação" que você copiou do n8n.
6.  Clique em "**Register application**".
7.  **Copie** o "**Client ID**" do GitHub e cole-o no campo "Client ID" das credenciais do n8n.
8.  **Gere um novo** "**Client Secret**" no GitHub, copie-o e cole-o no campo "Client Secret" das credenciais do n8n.
9.  Finalize clicando em "**Connect**" no n8n para autorizar o GitHub a interagir com sua instância.

### 2. Criar um Repositório GitHub para Backup

1.  No GitHub, crie um **novo repositório** (sugestão: `n8n-workflows-backup`).
2.  Você pode torná-lo **privado** para maior segurança.
3.  **(Opcional)** Para evitar erros iniciais no fluxo n8n, crie um arquivo de exemplo (ex: `example.json`) diretamente no seu novo repositório.

### 3. Configurar Credenciais da API n8n

1.  No n8n, vá para "**Settings**" > "**API Keys**" e clique em "**Generate New API Key**".
2.  **Copie** a chave da API gerada.
3.  No n8n, em "**Credenciais**", adicione uma nova credencial.
4.  Procure por "**n8n API**" e selecione-o.
5.  Cole a chave da API no primeiro campo.
6.  No campo "**Base URL**", insira a URL da sua instância n8n **seguida por `/api/v1`** (ex: `https://seu-n8n-instance.com/api/v1`).

### 4. Importar e Configurar o Fluxo de Backup n8n

1.  Você precisará construir ou obter o **arquivo JSON do fluxo de backup** (o vídeo de referência demonstra a estrutura). Os nós essenciais incluem:
    * **Gerar Data e Hora**: Para criar mensagens de commit informativas.
    * **Listar Arquivos no Repositório**: Para verificar quais fluxos já existem no GitHub.
    * **Transformar Saída GitHub**: Para processar a lista de arquivos.
    * **Obter Fluxos n8n**: Para extrair todos os seus fluxos da instância n8n.
    * **Mover para Binário**: Para converter os fluxos JSON em arquivos prontos para o GitHub, com nomes únicos (ex: `nome-do-fluxo-id-do-fluxo.json`).
    * **Upload Condicional**: Um nó inteligente que **atualiza** fluxos existentes e **cria** novos fluxos no GitHub.
2.  No n8n, crie um novo fluxo e **importe o arquivo JSON**.
3.  Configure os nós do fluxo com as credenciais GitHub e n8n API que você configurou anteriormente.
4.  Para testes, ative a opção "**Save Manual Executions**" nas configurações do fluxo.
5.  Adicione um nó "**Schedule Trigger**" ao fluxo para agendar **backups automáticos** (diariamente, semanalmente, etc.).

---

## ▶️ Execução e Teste

1.  **Execute** o fluxo de backup no n8n.
2.  Verifique seu **repositório GitHub** para confirmar se os arquivos dos seus fluxos n8n foram adicionados corretamente.
3.  Para um teste completo, crie um **novo fluxo de teste** no n8n e **execute o fluxo de backup novamente** para garantir que o novo fluxo seja adicionado ao repositório.

---

## ↩️ Restauração de Fluxos

Precisa restaurar um fluxo? É simples!

1.  No GitHub, navegue até o **arquivo JSON** do fluxo que você deseja restaurar.
2.  **Copie** todo o conteúdo do arquivo JSON.
3.  No n8n, crie um **novo fluxo vazio**.
4.  **Cole** o conteúdo JSON copiado diretamente na tela do fluxo n8n.
5.  **Renomeie e salve** o fluxo restaurado.

---

Este README foi gerado com base nas informações do vídeo: [https://www.youtube.com/watch?v=dNuVuoPD0Jo](https://www.youtube.com/watch?v=dNuVuoPD0Jo)
