# Base de Dados Jurídica Brasileira com o Repositório Leis

Este guia ensina passo a passo como baixar, organizar e utilizar o repositório ctresb/leis como base de dados jurídica para consultas, aplicações web, RAG (Retrieval-Augmented Generation), motores de busca e projetos de Inteligência Artificial. 【1-064133】

---

# Objetivo

Ao final deste tutorial você terá:

✅ Uma cópia local da legislação brasileira

✅ Um ambiente preparado para consultas

✅ Estrutura para projetos de IA

✅ Base pronta para PostgreSQL, ChromaDB ou Qdrant

✅ Organização profissional do projeto

---

# O que é este repositório?

O projeto ctresb/leis converte legislação brasileira para o formato Markdown.

Entre os conteúdos disponíveis estão:

- Constituição Federal
- Leis Ordinárias Federais
- Leis Complementares
- Decretos-Lei
- Legislação Estadual
- Emendas Constitucionais

Todos organizados em pastas e arquivos estruturados para fácil processamento por software. 【1-064133】

---

# Pré-requisitos

Instale os seguintes programas:

## Git

Download:

https://git-scm.com/download/win

Verifique a instalação:

```bash
git --version
```

Resultado esperado:

```text
git version x.x.x
```

---

## Python

Download:

https://python.org

Verifique:

```bash
python --version
```

Resultado esperado:

```text
Python 3.11.x
```

---

## Visual Studio Code

Download:

https://code.visualstudio.com

---

# Passo 1 - Criar a pasta de projetos

Escolha um local onde ficará o projeto.

Exemplo:

```text
C:\Projetos
```

Criar pelo PowerShell:

```powershell
mkdir C:\Projetos
```

Entrar na pasta:

```powershell
cd C:\Projetos
```

Verificar local atual:

```powershell
pwd
```

Resultado:

```text
C:\Projetos
```

---

# Passo 2 - Criar a pasta da aplicação

Criar uma pasta para hospedar todo o projeto:

```powershell
mkdir BaseLeis
```

Entrar nela:

```powershell
cd BaseLeis
```

Estrutura atual:

```text
C:\Projetos
└── BaseLeis
```

---

# Passo 3 - Clonar o repositório

Executar:

```bash
git clone https://github.com/ctresb/leis.git
```

O Git fará o download completo do repositório para sua máquina. O repositório contém legislação brasileira em formato Markdown organizada por esfera e tipo normativo. 【1-064133】

Estrutura resultante:

```text
C:\Projetos
└── BaseLeis
    └── leis
```

---

# Passo 4 - Entrar no repositório

```powershell
cd leis
```

Listar os arquivos:

```powershell
dir
```

Você deverá encontrar arquivos semelhantes a:

```text
README.md
COBERTURA.md
constituicao.md
federal
estaduais
scripts
```

O projeto possui a Constituição Federal, legislação federal, legislação estadual e scripts utilizados para coleta e conversão dos textos legais. 【1-064133】

---

# Passo 5 - Abrir no VS Code

Dentro da pasta:

```powershell
code .
```

O VS Code abrirá o projeto completo.

---

# Passo 6 - Entendendo a estrutura

Exemplo simplificado:

```text
leis/
│
├── constituicao.md
│
├── federal/
│   ├── leis-ordinarias/
│   ├── leis-complementares/
│   ├── leis-delegadas/
│   └── decretos-lei/
│
├── estaduais/
│   ├── SP/
│   ├── RJ/
│   ├── PE/
│   └── ...
│
└── scripts/
```

Essa organização permite localizar rapidamente qualquer norma por esfera governamental, categoria e ano. 【1-064133】

---

# Passo 7 - Estrutura recomendada para o projeto

Volte à pasta principal:

```powershell
cd ..
```

Crie as pastas auxiliares:

```powershell
mkdir app
mkdir banco
mkdir scripts
mkdir dados
mkdir docs
```

Resultado:

```text
BaseLeis
│
├── leis
├── app
├── banco
├── scripts
├── dados
├── docs
└── README.md
```

Descrição:

```text
leis      → legislação baixada
app       → aplicação principal
banco     → ChromaDB, Qdrant ou PostgreSQL
scripts   → importadores e processamentos
dados     → arquivos gerados
docs      → documentação
```

---

# Passo 8 - Criar ambiente virtual Python

Dentro de BaseLeis:

```bash
python -m venv .venv
```

Ativar:

PowerShell:

```powershell
.venv\Scripts\activate
```

O terminal mostrará:

```text
(.venv)
```

---

# Passo 9 - Instalar dependências

```bash
pip install chromadb
```

```bash
pip install sentence-transformers
```

```bash
pip install langchain
```

```bash
pip install pypdf
```

```bash
pip install pandas
```

---

# Passo 10 - Como os dados estão estruturados

Cada lei possui cabeçalho YAML.

Exemplo:

```yaml
---
titulo: "Lei nº 10406"
tipo: "Lei Ordinária"
numero: "10406"
data: "2002-01-10"
ementa: "Institui o Código Civil"
---
```

Após o cabeçalho vem o texto integral da norma. 【1-064133】

---

# Passo 11 - Pesquisa simples

Criar:

```text
scripts/pesquisa.py
```

Conteúdo:

```python
from pathlib import Path

base = Path("./leis")

termo = input("Pesquisar: ").lower()

for arquivo in base.rglob("*.md"):
    texto = arquivo.read_text(
        encoding="utf-8",
        errors="ignore"
    )

    if termo in texto.lower():
        print(arquivo)
```

Executar:

```bash
python scripts/pesquisa.py
```

---

# Passo 12 - Utilizando com IA

Fluxo recomendado:

```text
Leis Markdown
      ↓
Leitura dos arquivos
      ↓
Divisão em chunks
      ↓
Embeddings
      ↓
Banco vetorial
      ↓
Ollama/OpenAI/Claude
      ↓
Chat Jurídico
```

---

# Passo 13 - Atualizar a legislação

Quando houver atualizações:

```bash
cd leis
```

Depois:

```bash
git pull
```

Isso sincronizará sua cópia local com o repositório original. 【1-064133】

---

# Estrutura Final Recomendada

```text
BaseLeis
│
├── leis
│
├── app
│
├── banco
│
├── dados
│
├── docs
│
├── scripts
│
├── .venv
│
└── README.md
```

---

# Próximos Passos

Depois de concluir esta instalação você poderá:

- Criar um buscador jurídico.
- Construir um chatbot jurídico.
- Alimentar o Claude Code com a legislação.
- Criar uma API de consultas legais.
- Integrar PostgreSQL + pgvector.
- Integrar Qdrant.
- Integrar ChromaDB.
- Construir uma aplicação RAG completa baseada na legislação brasileira.

---

# Referência

Repositório oficial:

https://github.com/ctresb/leis

Projeto: ctresb/leis. 【1-064133】
