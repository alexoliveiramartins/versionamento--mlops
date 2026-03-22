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

## Referencias

[IBM Data Science - Best Practices](https://ibm.github.io/data-science-best-practices/versioning.html)
