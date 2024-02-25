# Laboratório DIO - Azure Cognitive Search: Utilizando AI Search para indexação e consulta de Dados
> [!NOTE]
> É necessário ter uma conta do Azure
## Passo a passo 
### 1. Criando um recurso 
  - No [Portal do Azure](https://portal.azure.com/#home)
  - No menu de cima click em **criar recurso**
    - Selecione o recurso *Azure AI Search*
    - Preencher
    - Na **Camada de preços** selecionar o *nível básico*
    - **Revisar e criar**
    - **Criar**
  - Volte para a tela principal
  - No menu de cima click em **criar recurso**
    - Selecione o recurso *Serviços Cognitivos*
    - Preencher
    - **Revisar e criar**
    - **Criar**
  - Volte para a tela principal
### 2. Criando e configurando uma Conta de armazenamento
  - No menu de cima click em **Contas de armazenamento**
  - **Criar**
  - Preencha os campos de **Assinatura** **Grupo de recursos** **Nome da conta de armazenamento** e **Região**
  - Selecione no **Desempenho** o *Standard*
  - Selecione na **Redundância** o *LRS*
  - **Examinar**
  - **Criar**
  - **Ir para recurso**
  - No menu lateral click em **Configuração**
    - Selecione no **Permitir acesso anônimo ao Blob** *Habilitado*
    - **Salvar**
  - No menu lateral click em **Contêineres**
  - Click em **+ Contêiner**
    - Preencha o **nome** como *coffereviews*
    - Selecione em **Nível de acesso anônimo** o campo *Contêiner*
    - **Criar**
  - Acesse o **coffereviews**
  - Faça o dowload do arquivo zipado no link de [exemplos de reviews](https://aka.ms/mslearn-coffee-reviews)
  - Extraia a pasta
  - Na página faça o **upload** do arquivo
### 3. Importação dos dados para o AI Search
  - Na página do seu recurso do AI Search
  - No menu de cima click em **Importar dados**
  - Em **Fonte de dados** selecione *Armazenamento de Blob do Azure*
  - Em **Nome da fonte de dados** preencha *coffe-costumer-data*
  - Em **Cadeia de conexão** click *Escolher uma conexão existente*
  - Selecione o armazenamento criado
  - Selecione **coffee-reviews**
  - **Selecionar**
  - Deixe o resto como padrão
  - **Avançar**
  - Em **Anexar Serviços de IA** selecione o seu recurso criado
  - Em **Adicionar enriquecimento**
      - Em **Nome do conjunto de habilidades** preencher como *coffee-skillset*
      - Selecione o checkbox **Habilitar OCR e mesclar todo o texto no campo merged_content**
      - Em **Nível de granularidade do enriquecimento** selecionar *Paginas(partes de caractere de 5000)*
      - Selecionar os checkbox de **Extrair nomes de localização locations**, **Extrair frases-chave keyphrases**, **Detectar sentimento sentiment**, **Gerar marcações de imagens imageTags**, **Gerar legendas de imagens imageCaption**
      - Em **Salvar os enriquecimentos em um repositório de conhecimento** selecionar **Projeções de imagem**, **Projeções de tabela do Azure**, **Documentos**, **Páginas**, **Frases-chave**, **Entidades**, **Detalhes da imagem**, **Referências de imagem**
      - Em **Projeções de blob do Azure** selecione **Documento**
      - **Próximo**
  - Preencha o **Nome do índice** como *coffee-index*
  - Selecione o checkbox do **Filtrável** em todos os capos que já estiverem marcados
  - **Próximo**
  - Preencha o **Nome** como *coffee-indexer*
  - **Agenda** uma vez
  - **Opções avançadas**
    - Selecione **Chaves de Codificação de Base 64**
    - Enviar
  - Em **Gerenciador de pesquisa**
  - Mude **Exibir** para **Exibição JSON**
  - Copie o código a seguir para pesquisar todas as reviews
    ```
    {
      "search": "*",
      "count": true
    }
    ```
  - Copie o código a seguir para pesquisar as reviews de Chicago
    ```
    {
     "search": "locations:'Chicago'",
     "count": true
    }
    ```
  - Copie o código a seguir para pesquisar todas as reviews negativas
    ```
    {
     "search": "sentiment:'negative'",
     "count": true
    }
    ```
