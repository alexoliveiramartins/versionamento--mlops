# Git, GitHub, GitFlow e Estruturação de Repositórios em MLOps

## 1️⃣ Motivação (~5 min)

### 1.1 Por que versionar em ML?

- Reprodutibilidade: É essencial no contexto de produções científicas e permite verificar como um modelo foi gerado ou explicar o comportamento de um modelo;
- Controle sobre os dados: O versionamento permite rastrear qual conjunto foi usado para treinar cada modelo - algo essencial para debugging e auditoria.

### 1.2 Diferenças entre software tradicional e ML

- Diferente de projetos de software tradicionais onde o versionamento é apenas de código, o versionamento em projetos de Machine Learning ocorre em 3 entidades: **Código, Dados e Modelos**

#### Dados: Mudam com frequencia e impactam diretamente o modelo de Machine Learning

- E qual o problema de versionar dados?
  > Muito grandes para Git
  > Mudanças difíceis de rastrear manualmente
- Por isso o versionamento de dados é feito usando outras ferramentas como: DVC (Data Version Control), LakeFS

#### Modelos: São o produto dos dados + código

- Modelos são armazenados em arquivos binários (.pt, .h5, .pkl)
- Git não funciona bem com binários:
  > Cada binário é um arquivo novo praticamente
  > Não gera diffs uteis para análise
  > Cada modelo novo adiciona muito peso ao repositório
- Alternativas para versionamento de dados e modelos: **Git LFS**, **DVC**, **MLflow**
  > Versionamento de dados vai ser discutido na apresentação do dia 05/08/2026 - Data Version Control (DVC)
  > Versionamento de modelos vai ser discutido na apresentação do dia 02/09/2026 - Model Registry (Repositórios)

### 1.3 Impacto prático

- Facilita colaboração e revisão, garantindo reprodutibilidade
- Dá base para CI/CD e deploy seguro

---

## 2️⃣ Como Funciona o Git (~15 min)

- O Git foi criado por Linus Torvalds para ajudar no desenvolvimento do Kernel do Linux
- Nos sistemas anteriores de versionamento de código, o versionamento era centralizado
- Em sistemas de versionamento centralizado, apenas um desenvolvedor podia trabalhar em um arquivo por vez -> Isso evitava conflitos de merge
- No git, por outro lado, o repositório é descentralizado

### 2.1 Conceitos fundamentais

- O Git armazena as versões dos arquivos dentro de um diretório
  > Esse histórico fica na pasta .git, dentro do diretório
- HEAD: Ponteiro para o último commit do repositório
- O Git armazena versões de arquivos baseados em snapshots
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
- Git stash: Armazena temporariamente suas mudanças (Bom para trazer mudanças não comitadas para outra branch)

### 2.3 GitHub e colaboração

- Github é um servidor que hospeda repositórios. Existem outros servidores como GitLab (pode ser self-hosted), BitBucket, etc.
- O repositório no GitHub serve como **fonte da verdade** para os desenvolvedores
- Possui configurações de acessos, fórums de discussão (issues) e pull requests para colaboração em projetos
- Automatiza pipelines de CI com testes apos cada push

### 2.5 Branches e Git merge

### 2.6 Estratégias de branching (~10 min)

- Quando trabalhamos em repositórios com muitos colaboradores, é essencial manter a organização das branches para que não haja conflitos e evitar que código quebrado não entre em produção

#### Git Flow

- Introduz as branches main/master, develop, hotfix, feature
  > main: Código em produção
  > hotfix: Branch que sai da main para hotfixes em produção, usada em casos emergenciais
  > develop: Branch da main com features que ainda não foram mergeadas
  > feature: Branches individuais de features que são integradas na develop
- Não é indicado para projetos onde há entrega contínua, pois as branches tem vida longa

#### Trunk-based

- Desenvolvedores colaboram em uma única branch
- As mudanças são pequenas e integradas na branch main frequentemente
- Utiliza **feature flags** para integrar features que ainda não foram totalmente finalizadas sem quebrar o código em produção
- Depende muito de pipelines de CI para validar integrações de código
- Ideal para entrega contínua/desenvolvimento rápido

#### Github Flow

- Workflow baseado em pull requests
- Similar ao Trunk-based
- Branches de features saem diretamente da master/main
- Integração de código é feita com pull requests
- Pull requests são revisados/discutidos e testados antes de serem mergeados

## 3️⃣ Quickstart (~10 min)

### 3.1 Boas práticas

#### Organização de repositórios em ML

- Uma organização clara de repositório é essencial em projetos de Data Science/Machine Learning
- Uma convenção comum para esse tipo de projeto é o template do **Cookiecutter Data Science**

Ajustar/traduzir esse template!

```bash
├── LICENSE            <- Open-source license if one is chosen
├── Makefile           <- Makefile
├── README.md          <- The top-level README for developers using this project.
├── data
│   ├── external       <- Data from third party sources.
│   ├── interim        <- Intermediate data that has been transformed.
│   ├── processed      <- The final, canonical data sets for modeling.
│   └── raw            <- The original, immutable data dump.
├── docs               <- A default mkdocs project.
├── models             <- Trained and serialized models, model predictions, or model summaries
├── notebooks          <- Jupyter notebooks
├── pyproject.toml     <- Project configuration file with package metadata
├── references         <- Data dictionaries, manuals, etc.
├── reports            <- Generated analysis as HTML, PDF, LaTeX, etc.
│   └── figures        <- Generated graphics and figures to be used in reporting
├── requirements.txt   <- The requirements file for reproducing the analysis
├── setup.cfg          <- Configuration file for flake8
└── src                <- Source code for use in this project.
    ├── __init__.py             <- Makes src a Python module
    ├── config.py               <- Store useful variables and configuration
    ├── dataset.py              <- Scripts to download or generate data
    ├── features.py             <- Code to create features for modeling
    ├── modeling
    │   ├── __init__.py
    │   ├── predict.py          <- Code to run model inference with models
    │   └── train.py            <- Code to train models
    └── plots.py                <- Code to create visualizations
```

#### **Commits semânticos** e mensagens de commit claras

#### Higiene de Commits

#### Organização do Histórico de commits

#### Usar o `.gitignore` de forma correta

#### Usar tags e releases

#### Documentação

### Ideia de exercício prático

- Simular um merge conflict e resolver ao vivo
- Ensinar como reverter commit do `.env`

## Referencias

- [IBM Data Science - Versioning Best Practices](https://ibm.github.io/data-science-best-practices/versioning.html)
- [Documentação oficial do git](https://git-scm.com/docs)
- [Cookiecutter Data Science - ML Directory structure](https://cookiecutter-data-science.drivendata.org/)
- [Git Flow Cheat Sheet (pt-BR)](https://danielkummer.github.io/git-flow-cheatsheet/index.pt_BR.html)
