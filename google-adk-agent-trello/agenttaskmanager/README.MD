<h1 align="center">Agente Inteligente para Gestão do Trello</h1>

<p align="center">
  Agente autônomo desenvolvido para gerenciar, analisar e interagir com quadros do <strong>Trello</strong> através de Inteligência Artificial e processamento de linguagem natural.
</p>

---

### Tecnologias e Frameworks Utilizados

<p align="left">
  <img src="https://img.shields.io/badge/-Python-333333?style=flat&logo=python" />
  <img src="https://img.shields.io/badge/-Trello%20API-333333?style=flat&logo=trello" />
  <img src="https://img.shields.io/badge/-Google%20ADK-333333?style=flat&logo=google" />
  <img src="https://img.shields.io/badge/-Google%20Gemini-333333?style=flat&logo=googlegemini" />
</p>

Este projeto utiliza um fluxo de integração de APIs em **Python**, com foco em automação e gerenciamento inteligente de tarefas via Inteligência Artificial:

- **Python**: Linguagem principal para orquestração, lógica e chamadas de API.
- **Trello API (REST / py-trello)**: Para comunicação direta com a plataforma, permitindo leitura e escrita de quadros, listas e cartões.
- **Framework de Agentes (Google ADK)**: Framework para criar o agente de IA e fornecer as ferramentas ("tools") de interação com o Trello.
- **LLM (Google Gemini)**: Motor cognitivo (`gemini-2.5-flash`) para interpretar o pedido do usuário e decidir qual ação tomar no Trello (ex: criar card, mover tarefa, resumir quadro).

---

### Componentes do Projeto

- **🔌 Integração com Trello (Ferramentas/Tools)** Responsável por autenticar com a API do Trello usando API Key e Token. Contém as funções utilitárias que buscam listas, criam cartões, adicionam descrições e movem tarefas entre as colunas.

- **🧠 Agente de IA Conversacional** Cria uma interface inteligente. É alimentado com um prompt de sistema (system prompt) que o instrui a agir como um Product Manager ou Scrum Master, capaz de entender comandos em texto livre e traduzi-los para chamadas na API.

- **⚙️ Orquestração do Fluxo** O laço principal de execução onde o usuário insere os comandos e o agente devolve o resultado após interagir com o Trello.

---

### Estrutura de Configuração e Entrada

O agente requer configurações de ambiente para funcionar corretamente com as APIs externas:

| Arquivo / Variável         | Descrição                                                  |
|----------------------------|------------------------------------------------------------|
| `.env`                     | Arquivo de variáveis de ambiente contendo chaves secretas. |
| `TRELLO_API_KEY`           | Chave de desenvolvedor da API do Trello.                   |
| `TRELLO_TOKEN`             | Token de autorização para acessar os quadros do usuário.   |
| `GOOGLE_API_KEY`           | Chave de API do provedor do modelo de linguagem (Google Gemini). |

---

### Arquitetura Geral do Fluxo

`Prompt do Usuário (Texto)` → `Agente de IA processa a intenção` → `Agente aciona a Tool do Trello` → `Trello API executa a ação (ex: Cria Card)` → `[Saída: Feedback ao Usuário via Chat]`

---

### Etapas do Funcionamento

1.  **Autenticação e Inicialização**
    -   O script carrega as credenciais do `.env` e inicializa a conexão com a API do Trello e o LLM escolhido.

2.  **Mapeamento de Ferramentas (Tool Binding)**
    -   As funções Python que interagem com o Trello (ex: `criar_cartao`, `listar_tarefas_pendentes`) são transformadas em ferramentas utilizáveis pelo agente.

3.  **Interação com o Usuário**
    -   O agente aguarda instruções. O usuário pode fazer pedidos complexos, como:
        -   *"Crie um card chamado 'Revisar documentação' na lista 'To Do' do quadro 'Projeto X'."*
        -   *"Quais são as tarefas atrasadas no quadro atual?"*

4.  **Execução e Retorno**
    -   O agente identifica a necessidade, aciona a API do Trello, coleta a resposta de sucesso/falha e formula uma resposta natural de volta para o usuário informando que a ação foi concluída.

---

### 📊 Saídas do Projeto

1.  **Ações no Trello**: Cartões criados, atualizados, comentados ou movidos automaticamente nos seus quadros reais.
2.  **Análises do Agente**: Resumos de produtividade, relatórios de gargalos e listagem de tarefas respondidas em texto pelo terminal/interface.

---
Autor:
Arthur Neves de Oliveira Santos
