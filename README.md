# Configuração de Pesquisa no Microsoft Azure

**Este é um trabalho foi desenvolvido para um desafio do BootCamp Decola Tech da DIO.**

Este documento fornece um guia passo a passo para configurar uma pesquisa no Microsoft Azure, explorando insights, ferramentas que podem se beneficiar dessa solução e aprendizados adquiridos durante o processo.

## Índice
1. [Introdução](#introdução)
2. [Requisitos](#requisitos)
3. [Passo a Passo para Configuração](#passo-a-passo-para-configuração)
4. [Ferramentas Beneficiadas](#ferramentas-beneficiadas)
5. [Insights e Aprendizados](#insights-e-aprendizados)
---

## Introdução
O Microsoft Azure oferece um serviço robusto de pesquisa chamado **Azure Cognitive Search**, que permite criar índices personalizados para facilitar a recuperação de informações de diferentes fontes de dados, incluindo o Cognitive Services - OCR, que permite o reconhecimento de texto em imagens. Combinado com o Azure Cognitive Search, é possível indexar e pesquisar documentos enriquecidos com OCR, tornando a busca mais eficiente e inteligente. Esse serviço é especialmente útil em cenários como digitalização de documentos, análise de conteúdo visual e construção de soluções baseadas em dados extraídos de imagens.

## Requisitos
Antes de iniciar a configuração, certifique-se de ter:
- Uma conta no **Microsoft Azure** ([Criar conta gratuita](https://azure.microsoft.com/pt-br/free/))
- Um recurso de **Azure Cognitive Search** provisionado
- Uma fonte de dados compatível (SQL Server, Blob Storage, CosmosDB, etc.)

## Passo a Passo para Configuração

### 1. Criar um Recurso Azure AI Search
1. Acesse o [Azure Portal](https://portal.azure.com/).
2. Crie um recurso **Azure AI Search** com as configurações:
   - Assinatura e grupo de recursos.
   - Nome único e região.
   - Plano **Basic**.
3. Confirme a criação e acesse o recurso.

### 2. Criar um Recurso Azure AI Services
1. Crie um recurso **Azure AI Services** na mesma região do Azure AI Search.
2. Escolha o plano **Standard S0** e confirme a criação.

### 3. Criar uma Conta de Armazenamento
1. Crie um recurso **Storage Account**.
2. Selecione o mesmo grupo de recursos.
3. Escolha **Locally Redundant Storage (LRS)**.
4. Ative o acesso anônimo para blobs.

### 4. Upload de Documentos no Azure Storage
1. No menu esquerdo, vá até **Containers** e crie um container chamado `img-ocr` .
2. No container, faça o upload dos arquivos extraídos.

### 5. Indexação de Documentos no Azure AI Search
1. No **Azure AI Search**, vá para **Import data**.
2. Escolha **Azure Blob Storage** e configure:
   - Nome da fonte de dados: `img-ocr`.
   - Dados a extrair: Conteúdo e metadados.
   - Conecte-se ao container `img-ocr`.
3. Anexe o serviço Azure AI;
4. Ative OCR e enriqueça os campos **locations, keyphrases, sentiment, imageTags, imageCaption**.
   

### 6. Fazendo a análise
Pronto, agora é o momento de explorar. Volte para o o Azure AI Search, selecione sua pesquisa e clique em "Search Explorer"

![search-explorer-button](https://github.com/user-attachments/assets/9a113401-2f05-4102-8a5c-d9afd534e18b)


#### Buscar todos os documentos:
```json
{
    "search": "*",
    "count": true
}
```
Essa busca retorna todos os documentos no índice de pesquisa.
![search-explorer](https://github.com/user-attachments/assets/ab1a094a-1c85-41bc-98e1-cfec011a9349)

## Ferramentas Beneficiadas
- **Azure Cognitive Search**: Para melhorar a busca em documentos, permitindo consultas rápidas em grandes volumes de dados com texto extraído por OCR.
- **Azure Functions**: Para automatizar a extração de texto de novas imagens.
- **Aplicações Web e Mobile**: Integrar OCR para reconhecer texto em imagens e realizar buscas no backend.

## Insights e Aprendizados
Durante o processo de configuração, algumas lições importantes foram aprendidas:
- **Precauções na qualidade das imagens**: A clareza das imagens impacta diretamente a precisão do OCR. Textos desfocados ou com baixa qualidade podem resultar em erros de extração.
- **Utilização de OCR e Search juntos**: Integrar OCR com Azure Cognitive Search melhora a busca por dados extraídos de imagens, permitindo uma indexação eficiente.
- **Facilidade de integração**: O processo de integração de OCR com a plataforma de busca do Azure é simples, mas o processo de enriquecimento de dados exige atenção para configurar corretamente as habilidades.
- **Automatização de fluxo de trabalho**: A automação via **Azure Functions** é útil para realizar OCR em imagens sempre que novas forem carregadas no armazenamento.


Para mais detalhes, consulte a [documentação oficial](https://learn.microsoft.com/pt-br/azure/search/) do Azure AI Search.
