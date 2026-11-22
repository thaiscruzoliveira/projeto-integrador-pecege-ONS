# Projeto Integrador - Análise de Pico e Vale do SIN em 2025

## Sobre o projeto

Este projeto foi desenvolvido como parte do Projeto Integrador do curso de Análise de Dados.

A análise busca responder à seguinte pergunta:

> **Como varia a composição da geração para atendimento à carga entre os horários de pico e de vale no Sistema Interligado Nacional ao longo de 2025?**

São analisadas as gerações:

- hidráulica;
- térmica;
- eólica;
- solar;

além da carga e dos intercâmbios de energia.

---

## Perguntas da análise

A análise principal foi estruturada a partir das seguintes perguntas:

1. Em quais horários ocorrem os picos e vales diários?
2. Qual é a composição média da geração nessas condições?
3. Quais fontes apresentam maior diferença entre vale e pico?
4. Essa composição varia ao longo dos meses?
5. Existem períodos ou dias particularmente diferentes do padrão?

Também são realizadas análises complementares da carga líquida e da composição da geração por subsistema.

---

## Metodologia

A análise utiliza dados horários do Sistema Interligado Nacional (SIN) para o ano de 2025.

Para cada dia, foram definidos:

- **Pico:** instante de maior carga do dia;
- **Vale:** instante de menor carga do dia.

Matematicamente:

$$
C_{\text{pico},d} = \max_h(C_{d,h})
$$

$$
C_{\text{vale},d} = \min_h(C_{d,h})
$$

A partir desses instantes, foram comparadas as gerações hidráulica, térmica, eólica e solar.

Também foi calculada, para cada fonte, a diferença entre geração no pico e no vale:

$$
\Delta G_{f,d}
=
G_{f,\text{pico},d}
-
G_{f,\text{vale},d}
$$

---

## Principais resultados

Entre os principais resultados observados em 2025:

- **74,5% dos picos diários** ocorreram às **18h ou 19h**;
- **72,9% dos vales diários** ocorreram às **3h ou 4h**;
- a carga média foi de aproximadamente **90,9 GWmed nos picos** e **68,1 GWmed nos vales**;
- a diferença média entre vale e pico foi de aproximadamente **22,8 GWmed**;
- a geração hidráulica apresentou aumento médio de aproximadamente **21,9 GWmed** entre vale e pico;
- a participação hidráulica passou de aproximadamente **58,9% no vale para 68,7% no pico**;
- a participação eólica passou de aproximadamente **23,3% no vale para 16,0% no pico**;
- a amplitude média entre vale e pico foi de aproximadamente **23,8 GWmed nos dias úteis** e **20,2 GWmed nos finais de semana**.

Como análise complementar, os horários dos picos da carga bruta e da carga líquida coincidiram em aproximadamente **62,5% dos dias**, enquanto os horários dos vales coincidiram em apenas **1,4% dos dias**.

---

## Estrutura do projeto

```text
projeto-integrador/
│
├── dados/
│   ├── brutos/
│   └── processados/
│
├── notebook/
│   ├── 01_preparacao_dados.ipynb
│   └── 02_analise_pico_vale.ipynb
│
├── saidas/
│
├── apresentacao/
│
├── .gitignore
├── README.md
└── requirements.txt
```

---

## Notebooks

### 01_preparacao_dados.ipynb

Responsável pela preparação e validação dos dados:

- leitura da base original;
- caracterização da estrutura;
- diagnóstico de valores ausentes;
- verificação de duplicidades;
- validação da cobertura temporal;
- análise de validade e plausibilidade;
- validação da consistência entre SIN e subsistemas;
- validação do balanço energético;
- criação das variáveis temporais;
- cálculo da geração total;
- cálculo da carga líquida;
- cálculo das participações das fontes;
- geração da base processada.

A principal saída é:

```text
dados/processados/balanco_energia_2025_processado.csv
```

### 02_analise_pico_vale.ipynb

Responsável pelas análises do projeto:

- seleção dos dados do SIN;
- análise do perfil horário da carga;
- identificação dos picos e vales diários;
- identificação dos extremos anuais;
- distribuição dos horários de pico e vale;
- comparação da composição da geração;
- variação da geração entre vale e pico;
- composição média da geração hora a hora;
- análise mensal da composição;
- comparação entre dias úteis e finais de semana;
- análise complementar da carga líquida;
- análise complementar por subsistema;
- geração das visualizações.

---

## Como executar

### 1. Clonar ou baixar o projeto

Após obter os arquivos, abra a pasta `projeto-integrador` no VS Code.

### 2. Criar o ambiente virtual

Na raiz do projeto:

```powershell
python -m venv .venv
```

### 3. Instalar as dependências

No Windows, sem necessidade de ativar o ambiente pelo PowerShell:

```powershell
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
```

As principais dependências utilizadas são:

- pandas;
- NumPy;
- Matplotlib;
- Seaborn;
- Jupyter;
- ipykernel.

### 4. Selecionar o kernel

No VS Code/Jupyter, selecionar o interpretador localizado em:

```text
.venv\Scripts\python.exe
```

### 5. Executar a preparação dos dados

Executar primeiro:

```text
notebook/01_preparacao_dados.ipynb
```

Preferencialmente:

**Restart Kernel + Run All**

Ao final da execução, deve ser gerado:

```text
dados/processados/balanco_energia_2025_processado.csv
```

### 6. Executar as análises

Em seguida, executar:

```text
notebook/02_analise_pico_vale.ipynb
```

Esse notebook utiliza a base processada e gera as análises e visualizações do projeto.

---

## Saídas

Os gráficos gerados pelo notebook de análise são armazenados na pasta:

```text
saidas/
```

Entre as visualizações estão:

```text
01_perfil_horario_carga.png
02_horarios_pico_vale.png
03_variacao_geracao_pico_vale.png
04_composicao_horaria_geracao.png
05_composicao_percentual_horaria.png
06_composicao_mensal_pico_vale.png
07_amplitude_dias_uteis_fim_semana.png
08_carga_bruta_liquida.png
09_composicao_subsistemas.png
```

---

## Tecnologias utilizadas

- Python
- pandas
- NumPy
- Matplotlib
- Seaborn
- Jupyter Notebook
- Visual Studio Code
- Git
- GitHub

---

## Limitações

A análise está restrita ao ano de 2025 e possui caráter descritivo.

Não foram considerados aspectos como:

- disponibilidade individual das usinas;
- armazenamento e níveis dos reservatórios;
- restrições elétricas e hidráulicas;
- custos de operação;
- indisponibilidades;
- limites de rampa;
- decisões de despacho;
- incertezas de previsão.

Os resultados devem ser interpretados como uma análise exploratória do comportamento observado no período.

---

## Próximos passos

Como possíveis extensões do projeto:

- comparar os resultados de 2023, 2024 e 2025;
- aprofundar a análise por subsistema;
- analisar os intercâmbios entre os subsistemas;
- incorporar dados de disponibilidade das fontes;
- incorporar informações de armazenamento dos reservatórios;
- investigar os dias com maiores amplitudes entre pico e vale;
- aprofundar a análise de carga líquida;
- avaliar efeitos sazonais, feriados e eventos extremos.

---

## Reprodutibilidade

A estrutura do projeto foi desenvolvida para permitir a reprodução das análises a partir dos dados originais.

O fluxo esperado é:

```text
Dados brutos
    ↓
01_preparacao_dados.ipynb
    ↓
Base processada
    ↓
02_analise_pico_vale.ipynb
    ↓
Gráficos e resultados
```

Para validar a execução completa, recomenda-se executar os dois notebooks utilizando:

**Restart Kernel + Run All**

---

## Autor

**Thais Cruz de Oliveira**

Projeto Integrador - Curso de Análise de Dados