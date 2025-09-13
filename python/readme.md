<h1 align="center">Agente Inteligente para Cálculo de Vale Refeição (VR/VA)</h1>

<p align="center">
  Agente desenvolvido como solução para o <strong>Desafio 4</strong> do curso <strong>Agentes Autônomos com Redes Generativas</strong>, uma parceria entre a <a href="https://www.meta.com.br/">Meta</a> e a <a href="https://www.i2a2.com.br/">I2A2</a>.
</p>

---

### Tecnologias e Frameworks Utilizados

<p align="left">
  <img src="https://img.shields.io/badge/-Python-333333?style=flat&logo=python" />
  <img src="https://img.shields.io/badge/-Pandas-333333?style=flat&logo=pandas" />
  <img src="https://img.shields.io/badge/-LangChain-333333?style=flat&logo=langchain" />
  <img src="https://img.shields.io/badge/-OpenAI-333333?style=flat&logo=openai" />
  <img src="https://img.shields.io/badge/-Matplotlib-333333?style=flat&logo=matplotlib" />
</p>

Este projeto utiliza um fluxo de processamento de dados em **Python**, com foco em automação, aplicação de regras de negócio e análise interativa via Inteligência Artificial:

- **Python**: Linguagem principal para orquestração e lógica.
- **Pandas**: Para consolidação, limpeza e manipulação de múltiplas planilhas.
- **LangChain**: Framework para criar o agente de IA e conectá-lo aos dados processados.
- **OpenAI / OpenRouter API**: Fornece o modelo de linguagem (LLM) para interpretação e resposta em linguagem natural (ex: `mistralai/mistral-7b-instruct`).
- **Matplotlib**: Para a geração de relatórios visuais e gráficos.

---

### Componentes do Notebook

- **📊 Consolidação e Cálculo (Pandas)** Responsável por carregar mais de 10 planilhas, unificar os dados, limpar inconsistências (como nomes de sindicatos) e aplicar todas as regras de negócio para o cálculo do benefício.

- **🧠 Agente de IA para Análise (LangChain)** Cria uma interface conversacional sobre o DataFrame final. É alimentado com um prompt customizado que o torna um especialista na folha de benefícios, capaz de responder perguntas analíticas.

- **📈 Visualização de Dados (Matplotlib)** Gera gráficos, como o custo total por sindicato, para facilitar a visualização e a tomada de decisão.

---

### Estrutura dos Dados de Entrada

O agente consolida dados de diversas fontes, sendo as principais:

| Arquivo de Entrada         | Descrição                                                  |
|----------------------------|------------------------------------------------------------|
| `ATIVOS.xlsx`              | Lista de todos os funcionários ativos na empresa.          |
| `ADMISSAO_ABRIL.xlsx`      | Relação de novos funcionários admitidos no mês.            |
| `DESLIGADOS.xlsx`          | Relação de funcionários desligados e data de comunicação.  |
| `FÉRIAS.xlsx`              | Planilha com os dias de férias programados para cada um.   |
| `Base sindicato x valor.xlsx`| Tabela de referência com o valor diário do VR por sindicato.|
| `Base dias uteis.xlsx`     | Tabela de referência com os dias úteis do mês por sindicato.|
| `AFASTAMENTOS.xlsx`        | Lista de funcionários em afastamento.                      |
| `ESTAGIO.xlsx` / `APRENDIZ.xlsx` | Listas de matrículas a serem excluídas do cálculo. |

---

### Arquitetura Geral do Fluxo

`Planilhas Excel (.zip)` → `Leitura e Consolidação (Pandas)` → `Aplicação de Regras de Negócio` → `DataFrame Final (df_calculo)` → `[Saída 1: Relatório .xlsx]` & `[Saída 2: Agente de IA para Análise]`

---

### Etapas do Funcionamento

1.  **Carga e Consolidação**
    -   O notebook descompacta o arquivo `.zip` e carrega as 10+ planilhas em DataFrames do Pandas.

2.  **Limpeza e Mapeamento**
    -   Padroniza os nomes das colunas e realiza um mapeamento inteligente para corrigir nomes de sindicatos inconsistentes entre as bases.

3.  **Aplicação das Regras de Negócio**
    -   Calcula os `dias_a_pagar` com base nos dias úteis, descontando férias e zerando o benefício para funcionários desligados com aviso prévio específico.

4.  **Geração do Relatório Final**
    -   Cria a planilha `VR MENSAL 05.2025.xlsx` no layout exato exigido pelo fornecedor.

5.  **Análise Interativa com IA**
    -   O `create_pandas_dataframe_agent` do LangChain é inicializado com o DataFrame final, permitindo que o usuário faça perguntas como:
        -   *"Qual o custo total de VR para a empresa este mês?"*
        -   *"Liste os 5 sindicatos que geraram o maior custo para a empresa."*

---

### 📊 Saídas do Projeto

1.  **Planilha para o Fornecedor (`VR MENSAL 05.2025.xlsx`)**: Arquivo final pronto para envio, contendo os valores calculados para cada funcionário.
2.  **Análises do Agente de IA**: Respostas em texto a perguntas sobre os dados.
3.  **Gráficos Visuais**: Gráfico de barras mostrando o custo total de VR por sindicato.

Autor:
Arthur Neves de Oliveira
---
