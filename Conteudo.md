# Git, GitHub, GitFlow e Estruturação de Repositórios em MLOps

## 1️⃣ Motivação

## 1.1 Por que versionar em ML?

- Reprodutibilidade: É essencial no contexto de produções científicas e permite verificar como um modelo foi gerado ou explicar o comportamento de um modelo;
- Controle sobre os dados: O versionamento permite rastrear qual conjunto foi usado para treinar cada modelo: algo essencial para debugging e auditoria.

### 1.2 Diferenças entre software tradicional e ML

- Diferente de projetos de software tradicionais onde o versionamento é apenas de código, o versionamento em projetos de Machine Learning ocorre em 3 entidades: **Código, Dados e Modelos**

#### Dados: Mudam com frequencia e impactam diretamente o modelo de Machine Learning

- E qual o problema de versionar dados?
  > Muito grandes para Git
  > Mudanças difíceis de rastrear manualmente
- Por isso o versionamento de dados é feito usando outras ferramentas como: DVC (Data Version Control), LakeFS

#### Modelos: São o produto dos dados + código

- São armazenados em modelos binários (.pt, .h5, .pkl)
- Git não funciona bem com binários:
  > Cada binário é um arquivo novo praticamente
  > Não gera diffs uteis para análise
  > Cada modelo novo adiciona muito peso ao repositório
- São versionados em ferramentas como MLflow (Model Registry)
- Os arquivos binários do modelo são vinculados à metadados (pesos, hiperparâmetros, etc.)

---

> Versionamento de dados e modelos vai ser falado futuramente em outras apresentações

### 1.3 Impacto prático

- Facilita colaboração e revisão, garantindo reprodutibilidade
- Dá base para CI/CD e deploy seguro

## 2️⃣ Como Funciona o Git

- O Git foi criado por Linus Torvalds para ajudar no desenvolvimento do Kernel do Linux
- Nos sistemas anteriores de versionamento de código, o versionamento era centralizado
- Em sistemas de versionamento centralizado, apenas um desenvolvedor podia trabalhar em um arquivo por vez -> Isso evitava conflitos de merge
- No git, por outro lado, o repositório é descentralizado

### 2.1 Conceitos fundamentais

- O Git armazena as versões dos arquivos dentro de um diretório
  > Esse histórico fica na pasta .git, dentro do diretório
- O Git armazena versões de arquivos baseados no diff
  > Não são armazenadas cópias de arquivos, mas sim as diferenças entre eles
- Uma alteração no código é um **commit**
- Cada commit calcula uma diff entre a versão anterior e a nova versão
- Branches: Ramificações do código que não interferem entre si
  > É a parte mais difícil de lidar quando se escala um projeto
- Arquivo `.gitignore`: Indica padrões de arquivos que não devem ser versionados como arquivos de dados, arquivos de configuração de ambiente (Ex.: `.env`)

### 2.2 Comandos básicos de Git

- Git init: Inicializa um repositório dentro de um diretório
- Git clone: Clona um repositório
- Git add: Adiciona um ou vários arquivos em staging para serem commitados
- Git commit: Cria um commit no repositório
  > Git commit -m "mensagem de commit"
- Git push: Envia as alterações para o repositório remoto
- Git pull: Traz as alterações da branch do repositório remoto
  > --rebase: Faz rebase das suas alterações
  > --no-rebase: Faz merge das alterações do repositório remoto
  > --ff-only: Faz rebase apenas se for possivel um merge fast-forward (será falado de merge mais para frente)
- Git checkout branch: Faz checkout para outra branch

### 2.3 GitHub e colaboração

- Github é um servidor que hospeda repositórios. Existem outros servidores como GitLab (pode ser self-hosted), BitBucket, etc.
- O repositório no GitHub serve como **fonte da verdade** para os desenvolvedores
- Possui configurações de acessos, fórums de discussão (issues) e pull requests para colaboração em projetos
- Automatiza pipelines de CI com testes apos cada push

### 2.4 Organização de repositórios em ML

- Uma organização clara de repositório é essencial em projetos de Data Science/Machine Learning
- Uma convenção comum para esse tipo de projeto é o template do Cookiecutter Data Science

```
project_name/
│
├── data/
│   ├── raw/          # Original, immutable data
│   ├── interim/      # Intermediate processing steps
│   ├── processed/    # Cleaned, final datasets
│   └── external/     # Third-party data
│
├── notebooks/        # Jupyter notebooks (exploration, prototyping)
│
├── src/              # Core source code
│   ├── data/         # Data loading & preprocessing
│   ├── features/     # Feature engineering
│   ├── models/       # Training & inference
│   └── visualization/# Plotting & reporting
│
├── models/           # Saved trained models
├── reports/          # Generated reports, figures
├── configs/          # YAML/JSON config files
├── tests/            # Unit tests
│
├── requirements.txt  # Dependencies
├── environment.yml   # Conda environment (optional)
├── README.md
└── setup.py / pyproject.toml
```

### 2.5 Estratégias de branching

### 2.6 Git merge

## 3️⃣ Quickstart

## Boas práticas

- Commits semânticos e mensagens de commit claras

### Ideia de exercício prático

- Simular um merge conflict e resolver ao vivo

## Referencias

[IBM Data Science - Versioning Best Practices](https://ibm.github.io/data-science-best-practices/versioning.html)
[Documentação oficial do git](https://git-scm.com/docs)
[Cookiecutter Data Science - ML Directory structure](https://cookiecutter-data-science.drivendata.org/)
