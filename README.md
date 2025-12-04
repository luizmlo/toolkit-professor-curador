# 🎓 Kit do Professor Curador

Uma aplicação web Python que ajuda professores e educadores a planejarem aulas e lições usando pesquisa e geração de currículo com IA. O kit permite que você pesquise tópicos, organize o currículo em blocos estruturados e gere prompts otimizados para ferramentas educacionais como NotebookLM e Gamma.app.

## Funcionalidades

- **Pesquisa com IA**: Digite um tópico e obtenha uma lista curada de fontes de pesquisa (livros, artigos, ensaios)
- **Geração Inteligente de Currículo**: Gera automaticamente sub-tópicos organizados em dois blocos lógicos
- **Criação Manual de Currículo**: Adicione habilidades manualmente antes de gerar com IA
- **Editor Interativo de Currículo**: 
  - Reordenação de tópicos por arrastar e soltar
  - Edição de títulos e descrições de tópicos
  - Adicionar e remover tópicos
  - Dois blocos principais (Bloco 1: Fundamentos, Bloco 2: Aplicações Práticas)
- **Assistente de Chatbot**: Gerencie o currículo usando linguagem natural
  - Adicione, edite, remova ou reordene cards através de comandos
  - Receba perguntas de feedback após mudanças
- **Geração de Prompts**: Gera prompts otimizados para:
  - **inVideo AI**: Vídeos educativos de 60-90 segundos
  - **NotebookLM**: Guias de estudo analíticos
  - **ElevenLabs**: Roteiros de podcast estilo true crime educativo
  - **Google Colab**: Código Python para visualizações interativas
  - **Google Forms**: Questões de múltipla escolha com gabarito e explicações
- **Persistência de Sessões**: Salve e carregue seus currículos no navegador

## Tech Stack

- **Backend**: FastAPI (Python)
- **Frontend**: HTML, CSS, JavaScript (Vanilla JS)
- **IA**: Google Gemini API (Gemini 2.5 Flash)
- **Servidor**: Uvicorn

## Instalação

1. **Clone o repositório** (ou navegue até o diretório do projeto)

2. **Instale as dependências**:
   ```bash
   pip install -r requirements.txt
   ```

3. **Configure a Chave da API Gemini**:
   - Crie um arquivo `.env` no diretório raiz.
   - Adicione sua chave da API Gemini:
     ```
     GEMINI_API_KEY=sua_chave_gemini_aqui
     ```
   - Para obter sua chave, acesse o [Google AI Studio](https://aistudio.google.com)
   - **IMPORTANTE**: Nunca commite o arquivo `.env` com sua chave real!

## Uso

1. **Inicie o servidor**:
   
   Para desenvolvimento (com reload automático):
   ```bash
   python run.py
   ```
   
   Para produção:
   ```bash
   python app.py
   ```
   
   Ou usando uvicorn diretamente:
   ```bash
   uvicorn app:app --reload --host 0.0.0.0 --port 8000
   ```

2. **Abra seu navegador** e navegue para:
   ```
   http://localhost:8000
   ```

3. **Use a aplicação**:
   - **Criar Currículo**: Escolha entre criar manualmente, pesquisar fontes primeiro, ou gerar diretamente com IA
   - **Gerenciar Cards**: Adicione, edite, remova ou reordene habilidades usando a interface ou o assistente de chatbot
   - **Assistente de Chatbot**: Clique no botão flutuante 💬 para abrir o assistente e gerenciar o currículo com comandos em linguagem natural
   - **Gerar Prompts**: Clique em "📋 Prompts" em cada habilidade para gerar prompts personalizados para ferramentas educacionais
   - **Salvar Sessões**: Use "💾 Salvar Sessão" para persistir seu trabalho no navegador

## Estrutura do Projeto

```
a3-ia-2/
├── app.py                 # Aplicação backend FastAPI (API REST + IA)
├── run.py                 # Script de inicialização para desenvolvimento
├── requirements.txt       # Dependências Python
├── README.md             # Este arquivo
├── .gitignore            # Arquivos ignorados pelo Git
├── .env                  # Variáveis de ambiente (crie este, NÃO commitar!)
└── static/
    ├── index.html        # Interface HTML principal
    ├── styles.css        # Estilos CSS
    └── script.js         # Lógica JavaScript do frontend
```

## Endpoints da API

- `GET /` - Serve a página HTML principal
- `POST /api/research` - Pesquisa um tópico e encontra fontes de pesquisa
- `POST /api/generate-curriculum` - Gera sub-tópicos do currículo usando IA
- `POST /api/generate-method-card-prompt` - Gera prompt personalizado para ferramenta educacional
- `POST /api/chatbot` - Processa comandos em linguagem natural e retorna ações + perguntas de feedback

## Funcionalidades em Detalhe

### Fase de Pesquisa
O sistema usa Google Gemini para pesquisar seu tópico e identificar 8-12 fontes de pesquisa de alta qualidade, incluindo livros acadêmicos, artigos de pesquisa, artigos de revisão e ensaios importantes.

### Geração de Currículo
Com base no seu tópico e fontes de pesquisa, o sistema gera um currículo estruturado com:
- **Bloco 1 (Fundamentos)**: Conceitos fundamentais e básicos
- **Bloco 2 (Tópicos Avançados)**: Conteúdo mais complexo e especializado

Cada bloco contém 6-8 sub-tópicos com títulos e descrições.

### Editor de Currículo
- **Arrastar e Soltar**: Reordene tópicos dentro dos blocos ou mova-os entre blocos
- **Editar**: Clique em "Editar" para modificar títulos e descrições dos tópicos
- **Adicionar**: Clique em "+ Adicionar Tópico" para adicionar novos tópicos a qualquer bloco
- **Remover**: Clique em "Remover" para excluir tópicos

### Geração de Prompts (Method Cards)
O sistema gera 5 tipos de prompts otimizados:
1. **Vídeo Educativo (inVideo AI)**: Roteiro para vídeo educativo de 60-90 segundos
2. **Guia Teórico (NotebookLM)**: Guia de estudo analítico completo
3. **Estudo de Caso (ElevenLabs)**: Roteiro de podcast estilo true crime educativo
4. **Visualização Interativa (Google Colab)**: Código Python para laboratório virtual
5. **Quiz de Diagnóstico (Google Forms)**: Questões de múltipla escolha com gabarito e explicações

### Assistente de Chatbot
O assistente permite gerenciar o currículo usando linguagem natural:
- **Adicionar cards**: "Crie 5 cards sobre Python no bloco 1"
- **Editar cards**: "Edite o card sobre X para ter o título Y"
- **Remover cards**: "Remova o card sobre Z"
- **Reordenar**: "Mova o primeiro card para o final"
- **Feedback**: Após executar ações, recebe 3 perguntas de feedback contextualizadas

## Requisitos

- Python 3.8+
- Chave da API Gemini (obtenha em [Google AI Studio](https://aistudio.google.com))
- Conexão com a internet (para chamadas à API Gemini)

## Notas Importantes

- **Segurança**: A chave da API Gemini deve estar no arquivo `.env` (nunca commitar no código!)
- **Performance**: As chamadas à API usam Gemini 2.5 Flash para resultados rápidos e de alta qualidade
- **Armazenamento**: Dados são salvos apenas no LocalStorage do navegador (não há servidor de banco de dados)
- **Privacidade**: Todos os dados processados e salvos são locais, exceto chamadas à API Gemini

## Estrutura de Dados

### Sessão Salva (LocalStorage)
```json
{
  "id": "timestamp",
  "name": "Nome da Sessão",
  "topic": "Tópico do Currículo",
  "researchSources": [...],
  "curriculum": {
    "block1": [...],
    "block2": [...]
  },
  "methodCardPrompts": {...},
  "savedAt": "ISO timestamp",
  "updatedAt": "ISO timestamp"
}
```

## Licença

Este projeto é de código aberto e disponível para uso educacional.

## Solução de Problemas

- **"Erro ao pesquisar tópico"**: Verifique se sua chave da API Gemini está correta e configurada no arquivo `.env`
- **Porta já em uso**: Altere a porta em `app.py` ou use uma porta diferente com uvicorn
- **Módulo não encontrado**: Certifique-se de que todas as dependências estão instaladas com `pip install -r requirements.txt`
#
