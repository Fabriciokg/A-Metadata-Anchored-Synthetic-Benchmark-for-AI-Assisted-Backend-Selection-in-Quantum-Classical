# Benchmark Sintetico Ancorado em Metadados para Selecao de Backend Assistida por IA em Workflows Quantico-Classicos

Este repositorio contem o notebook, o artigo e os materiais de reprodutibilidade do trabalho:

**A Metadata-Anchored Synthetic Benchmark for AI-Assisted Backend Selection in Quantum-Classical Workflows**

O projeto avalia selecao de backend assistida por IA em workflows quantico-classicos usando um benchmark sintetico controlado, parcialmente ancorado em metadados reais do IBM/Qiskit Runtime.

O objetivo principal nao e demonstrar vantagem quantica, nem afirmar superioridade operacional em QPUs de producao. O objetivo e fornecer um framework reprodutivel para comparar estrategias de selecao de backend sob condicoes controladas de workload, backend, metricas operacionais e perfis de decisao.

---

## O que este repositorio contem

- Notebook completo para gerar o benchmark sintetico.
- Ancoragem parcial em metadados IBM/Qiskit Runtime para o perfil de QPU supercondutora.
- Modelos de predicao de tempo de execucao e fidelidade esperada.
- Classificacao de recomendacao de backend.
- Ranking final de backends e avaliacao por utility regret.
- Comparacao com heuristicas, weighted utility, TOPSIS, Pareto e rankers supervisionados.
- Analises de ablation, robustez, sensibilidade e plausibilidade externa.
- PDF do artigo associado.

---

## Estrutura do repositorio

```text
ai-quantum-backend-selection/
├── README.md
├── README.pt-BR.md
├── LICENSE
├── requirements.txt
├── environment.yml
├── .gitignore
├── .env.example
├── notebooks/
│   └── ai_quantum_systems_workload_orchestration_v9_6_live_ibm_required.ipynb
├── paper/
│   └── A_Metadata_Anchored_Synthetic_Benchmark_for_AI_Assisted_Backend_Selection_in_Quantum_Classical_Workflows.pdf
├── outputs/
│   └── README.md
└── docs/
    ├── IBM_QUANTUM_CREDENTIALS.md
    ├── REPRODUCIBILITY.md
    └── SECURITY.md
```

---

## Escopo cientifico

Este projeto trata a selecao de backend como um problema de decisao multicriterio em workflows quantico-classicos.

Uma politica de selecao de backend precisa considerar simultaneamente:

- tempo de execucao;
- fidelidade esperada;
- custo;
- condicoes de fila;
- disponibilidade do backend;
- probabilidade de falha;
- ruido e caracteristicas de calibracao;
- capacidade do dispositivo;
- necessidade de execucao em hardware real.

O notebook gera pares workload-backend sinteticos em diferentes familias de algoritmos e modalidades de execucao. Quando credenciais validas da IBM sao fornecidas, o perfil de QPU supercondutora e parcialmente ancorado em metadados vivos do IBM/Qiskit Runtime.

---

## Limitacao importante

Os labels de recomendacao sao gerados por uma funcao sintetica de utilidade multicriterio. Portanto, os modelos supervisionados aprendem a aproximar uma politica sintetica controlada, nao uma politica operacional verdadeira aprendida a partir de logs reais de execucao.

Os metadados IBM/Qiskit Runtime aumentam a plausibilidade externa de alguns atributos de backend, mas nao substituem validacao com logs de execucao em QPUs reais de producao.

A execucao em hardware real fica desabilitada por padrao. O notebook realiza verificacoes locais com Qiskit Aer e verificacoes de plausibilidade por metadados, mas nao deve ser interpretado como uma validacao completa em hardware real.

---

## Requisitos

Use Python 3.10 ou superior.

Instale as dependencias com:

```bash
pip install -r requirements.txt
```

---

## Credenciais IBM Quantum

O notebook usa credenciais IBM Quantum / Qiskit Runtime para coletar metadados vivos da IBM.

Voce precisa de dois valores:

1. `IBM_QUANTUM_TOKEN`: sua chave de API do IBM Cloud.
2. `IBM_QUANTUM_INSTANCE`: o CRN da sua instancia do IBM Quantum Runtime.

Nunca faca commit desses valores no GitHub, GitLab ou qualquer repositorio publico.

Crie um arquivo local `.env` a partir do exemplo:

```bash
cp .env.example .env
```

Depois edite `.env`:

```bash
IBM_QUANTUM_TOKEN=your_ibm_cloud_api_key_here
IBM_QUANTUM_INSTANCE=your_ibm_quantum_runtime_crn_here
```

Ou exporte as variaveis no terminal:

```bash
export IBM_QUANTUM_TOKEN="your_ibm_cloud_api_key_here"
export IBM_QUANTUM_INSTANCE="your_ibm_quantum_runtime_crn_here"
```

O guia completo esta em:

```text
docs/IBM_QUANTUM_CREDENTIALS.md
```

---

## Como executar

Depois de instalar as dependencias e configurar as credenciais, inicie o Jupyter:

```bash
jupyter notebook
```

Abra o arquivo:

```text
notebooks/ai_quantum_systems_workload_orchestration_v9_6_live_ibm_required.ipynb
```

Execute todas as celulas de cima para baixo.

Se as variaveis de ambiente nao estiverem definidas, o notebook pedira a chave IBM e o CRN de forma interativa.

---

## Saidas esperadas

O notebook gera os artefatos em:

```text
outputs_ai_quantum_v9_6/
```

As saidas incluem dataset gerado, catalogo de backends, sumarios de ancoragem, predicoes, rankings, comparacoes com baselines, metricas por subgrupo, analises de ablation, analises de sensibilidade e figuras.

---

## Aviso de seguranca

Nao publique:

- `.env`;
- chaves de API da IBM;
- CRNs, caso voce os considere sensiveis;
- arquivos locais de conta do Qiskit;
- caches de credenciais;
- logs privados de execucao;
- metadados pessoais da conta.

O arquivo `.gitignore` deste repositorio foi configurado para reduzir o risco de commits acidentais de credenciais.
