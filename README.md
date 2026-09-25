from pathlib import Path

readme = """# Python para Análise de Dados — Aulas 02, 03 e 04

Este repositório reúne uma sequência introdutória de aulas de **Python aplicado à Análise de Dados**, desenvolvida para apresentar lógica de programação de forma progressiva e conectada a situações práticas.

Ao longo das três aulas, o estudante evolui da construção de decisões simples com Python para a aplicação de regras em bases de dados e, posteriormente, para estruturas de repetição, automação e geração de indicadores de negócio.

---

## 📚 Conteúdo

- [Visão geral](#-visão-geral)
- [Aula 02 — Decisões com Python](#-aula-02--decisões-com-python)
- [Aula 03 — Condicionais aplicadas a dados](#-aula-03--condicionais-aplicadas-a-dados)
- [Aula 04 — Repetição e Automação](#-aula-04--repetição-e-automação)
- [Projeto Integrador](#-projeto-integrador)
- [Progressão da aprendizagem](#-progressão-da-aprendizagem)
- [Tecnologias utilizadas](#-tecnologias-utilizadas)
- [Competências desenvolvidas](#-competências-desenvolvidas)
- [Arquivos](#-arquivos)

---

# 🎯 Visão geral

A proposta das aulas é desenvolver fundamentos de programação importantes para quem está iniciando em **Análise de Dados com Python**.

A sequência trabalha três ideias centrais:

1. **Tomar decisões com base em condições**;
2. **Aplicar regras de negócio em conjuntos de dados**;
3. **Automatizar tarefas repetitivas e gerar indicadores**.

A progressão pode ser resumida como:

```text
Condição
   ↓
Decisão
   ↓
Aplicação em dados
   ↓
Repetição e automação
   ↓
Indicadores
   ↓
Interpretação de negócio
```

---

# 🟦 Aula 02 — Decisões com Python

**Arquivo:** `Aula_Python02.ipynb`

## Objetivo

Introduzir lógica booleana, operadores e estruturas condicionais, permitindo que o programa tome caminhos diferentes de acordo com determinadas condições.

## Conteúdos

### 1. Booleanos

Os valores booleanos representam dois estados:

```python
True
False
```

Exemplo:

```python
maior_de_idade = True
possui_cupom = False
```

---

### 2. Operadores relacionais

São utilizados para comparar valores e produzir resultados booleanos.

Exemplos trabalhados na aula:

```python
nota >= 7
frequencia >= 75
nota < 5
frequencia != 0
```

---

### 3. Operadores lógicos

A aula apresenta:

- `and` — exige que as condições sejam verdadeiras;
- `or` — exige que pelo menos uma condição seja verdadeira;
- `not` — inverte um resultado booleano.

Exemplo:

```python
nota = 6
frequencia = 80

aprovado = nota >= 7 and frequencia >= 75

print(aprovado)
```

---

## 📊 Aplicação prática: análise de churn

A aula utiliza um cenário de clientes para demonstrar como condições podem representar regras reais.

São consideradas informações como:

```python
plano_ativo
dias_sem_acesso
quantidade_reclamacoes
pagamento_em_atraso
```

A partir dessas variáveis, o programa identifica diferentes situações.

Exemplo:

```python
churn_confirmado = not plano_ativo

risco_churn = (
    plano_ativo
    and dias_sem_acesso >= 30
    and (
        quantidade_reclamacoes >= 2
        or pagamento_em_atraso
    )
)
```

---

## 🧩 Desafio da aula

Criar um **classificador de risco de churn** para uma empresa de streaming.

O cliente deve ser classificado como:

1. **Churn confirmado** — quando o plano não estiver ativo;
2. **Alto risco de churn** — quando o plano estiver ativo, estiver sem acessar há 30 dias ou mais e possuir pelo menos duas reclamações ou pagamento em atraso;
3. **Cliente precisa de atenção** — quando estiver entre 15 e 29 dias sem acessar;
4. **Cliente ativo e engajado** — quando nenhuma das condições anteriores ocorrer.

### Conceitos praticados

```text
Booleanos
      +
Operadores relacionais
      +
Operadores lógicos
      +
Condicionais
      ↓
Regra de negócio
```

---

# 🟩 Aula 03 — Condicionais aplicadas a dados

**Arquivo:** `Aula_Python03.ipynb`

## Objetivo

Aprofundar as decisões condicionais e aplicá-las a conjuntos de dados utilizando Python e Pandas.

## Conteúdos

### 1. Revisão de lógica booleana

A aula retoma:

```python
True
False
```

além de operadores relacionais:

```text
==  igual
!=  diferente
>   maior
>=  maior ou igual
<   menor
<=  menor ou igual
```

e operadores lógicos:

```python
and
or
not
```

---

## 2. Estrutura `if / else`

Utilizada quando existem dois caminhos principais.

```python
nota = 6

if nota >= 7:
    print('Aprovado')
else:
    print('Reprovado')
```

---

## 3. Estrutura `elif`

O `elif` permite testar outras condições quando a anterior não é atendida.

```python
nota = 8.9

if nota >= 7:
    print('Aprovado')
elif nota >= 5:
    print('Recuperação')
else:
    print('Reprovado')
```

---

# 🎓 Caso prático: desempenho de alunos

A aula utiliza o arquivo:

```text
alunos_desempenho.csv
```

O arquivo é carregado no Google Colab:

```python
from google.colab import files

uploaded = files.upload()
```

Em seguida, o Pandas é utilizado para ler os dados:

```python
import pandas as pd

arquivo = next(iter(uploaded))
df = pd.read_csv(arquivo)

df.head()
```

---

## Cálculo da média

Uma nova coluna é criada a partir das notas:

```python
df['media'] = (df['nota_1'] + df['nota_2']) / 2
```

---

## Função de classificação

A classificação considera média e frequência.

```python
def classificar(media, frequencia):
    if media >= 7 and frequencia >= 75:
        return 'Aprovado'

    elif media >= 5 and frequencia >= 75:
        return 'Recuperação'

    else:
        return 'Reprovado'
```

A função é aplicada às linhas do DataFrame:

```python
df['situação'] = df.apply(
    lambda linha: classificar(
        linha['media'],
        linha['frequencia']
    ),
    axis=1
)
```

### Fluxo da análise

```text
Arquivo CSV
    ↓
Pandas
    ↓
DataFrame
    ↓
Cálculo da média
    ↓
Regra condicional
    ↓
Classificação
```

---

# 🛒 Desafio Loja

O segundo exercício trabalha regras de desconto em uma base de pedidos.

Arquivo utilizado:

```text
pedidos_loja.csv
```

## Regras

- Cliente VIP recebe **15%**;
- Compra acima de **R$ 150** recebe **10%**;
- Cliente que utilizou cupom recebe **5%**;
- Demais casos não recebem desconto.

A função utilizada é:

```python
def desconto(valor, tipo_cliente, usou_cupom):
    if tipo_cliente == 'vip':
        return 0.15

    elif valor > 150:
        return 0.10

    elif usou_cupom == True:
        return 0.05

    else:
        return 0.00
```

A função é aplicada aos pedidos:

```python
pedidos['percentual_desconto'] = pedidos.apply(
    lambda linha: desconto(
        linha['valor_compra'],
        linha['tipo_cliente'],
        linha['usou_cupom']
    ),
    axis=1
)
```

Depois é calculado o valor final:

```python
pedidos['valor_final'] = (
    pedidos['valor_compra']
    * (1 - pedidos['percentual_desconto'])
).round(2)
```

A aula também apresenta uma alternativa sem `lambda`, utilizando uma função que recebe diretamente cada linha do DataFrame.

---

# 🟨 Aula 04 — Repetição e Automação

**Arquivo:** `Aula_Python04.ipynb`

## Objetivo

Introduzir estruturas de repetição para evitar tarefas manuais repetitivas e começar a automatizar análises.

## Conteúdos

- Listas;
- `for`;
- `range()`;
- Contadores;
- Acumuladores;
- `while`;
- Iteração em DataFrames;
- Indicadores de vendas;
- Relatório de negócio.

---

# 1. Listas

Listas armazenam vários valores em uma única variável.

```python
notas = [7.5, 8.0, 6.0, 9.0, 5.5, 7.9, 10.0, 8.1]

print(notas)
print(notas[7])
```

---

# 2. Estrutura `for`

O `for` percorre uma sequência de valores.

```python
nomes = ['Ana', 'Bruno', 'Carla', 'Tiago', 'Fabio']

for nome in nomes:
    print('Olá', nome)
```

---

# 3. `range()`

O `range()` cria sequências numéricas.

```python
for numero in range(1, 6):
    print(numero)
```

Também é possível definir um intervalo:

```python
for numero in range(1, 11, 2):
    print(numero)
```

---

# 4. Contadores

Um contador aumenta quando determinada condição acontece.

```python
notas = [7.5, 8.0, 6.0, 9.0, 5.5, 6.2, 9.0]

aprovados = 0
reprovados = 0

for nota in notas:

    if nota >= 7:
        aprovados += 1

    else:
        reprovados += 1

print('Aprovados:', aprovados)
print('Reprovados:', reprovados)
```

Nesse contexto:

```python
aprovados += 1
```

é equivalente a:

```python
aprovados = aprovados + 1
```

---

# 5. Acumuladores

O acumulador adiciona valores progressivamente.

```python
vendas = [1200, 2000, 600, 3500, 1800]

total = 0

for venda in vendas:
    total += venda

print('Total:', total)
```

---

# 6. Estrutura `while`

O `while` mantém a repetição enquanto uma condição for verdadeira.

```python
contador = 1

while contador <= 10:
    print(contador)
    contador += 1
```

## Quando utilizar?

### `for`

Quando existe uma sequência ou uma quantidade conhecida de elementos.

Exemplo:

```text
percorrer notas
percorrer clientes
percorrer produtos
```

### `while`

Quando a repetição depende de uma condição.

Exemplo apresentado na aula:

```text
continuar tentando enquanto a senha não estiver correta
```

---

# 📊 Projeto Integrador

## Relatório de vendas

Na etapa final da Aula 04 é utilizado:

```text
vendas_semana.csv
```

O objetivo é transformar uma base de vendas em um pequeno relatório analítico.

O projeto solicita:

1. Total de vendas;
2. Média diária;
3. Maior venda;
4. Quantidade de dias que atingiram a meta;
5. Conclusão em linguagem de negócio.

---

## Etapa 1 — Carregamento

```python
from google.colab import files

uploaded = files.upload()

import pandas as pd

arquivo = next(iter(uploaded))
df = pd.read_csv(arquivo)

df.head()
```

---

## Etapa 2 — Verificação inicial

Antes de analisar, é feita uma conferência da base:

```python
print('Quantidade de dias registrados:', len(df))

print('Valores ausentes por coluna:')
print(df.isna().sum())
```

Essa etapa verifica:

- quantidade de registros;
- existência de valores ausentes.

---

## Etapa 3 — Total de vendas

```python
total = df['vendas'].sum()

print(f'Total de vendas: R$ {total:.2f}')
```

---

## Etapa 4 — Média diária

```python
media = df['vendas'].mean()

print(f'Média diária: R$ {media:.2f}')
```

---

## Etapa 5 — Maior venda diária

```python
maior = df['vendas'].max()

print(f'Maior venda diária: R$ {maior:.2f}')
```

---

## Etapa 6 — Dias que atingiram a meta

```python
dias_meta = 0

for indice, linha in df.iterrows():

    if linha['vendas'] >= linha['meta']:
        dias_meta += 1

quantidade_dias = len(df)

print(
    f'Dias que bateram a meta: '
    f'{dias_meta} de {quantidade_dias}'
)
```

Essa etapa integra conteúdos de diferentes aulas:

```text
for
+
if
+
contador
+
DataFrame
```

---

## Etapa 7 — Meta semanal

```python
meta_semana = df['meta'].sum()

diferenca = total - meta_semana

print(f'Meta semanal: R$ {meta_semana:.2f}')
print(
    f'Diferença entre vendas e meta: '
    f'R$ {diferenca:.2f}'
)
```

---

## Etapa 8 — Interpretação dos resultados

A última parte do projeto transforma os indicadores em linguagem de negócio.

No exemplo desenvolvido no notebook:

- foram registrados **R$ 16.463,23** em vendas na semana;
- a média diária foi de **R$ 2.351,89**;
- a meta diária foi atingida ou superada em **4 dos 7 dias**;
- a terça-feira apresentou o maior valor vendido;
- as vendas ficaram **R$ 1.036,77 abaixo** da meta semanal de **R$ 17.500,00**.

> Observação: o notebook registra no texto final “R$ 1.306,77 abaixo”, mas os valores de R$ 16.463,23 em vendas e R$ 17.500,00 de meta resultam em uma diferença aritmética de R$ 1.036,77. O README mantém os valores do exemplo e sinaliza essa divergência para revisão.

---

# 🚀 Progressão da aprendizagem

As aulas foram organizadas de forma progressiva.

## Aula 02

O aluno aprende:

```text
Como o programa toma uma decisão?
```

Fluxo:

```text
Valores
  ↓
Comparação
  ↓
True / False
  ↓
Condição
  ↓
Decisão
```

---

## Aula 03

A pergunta evolui para:

```text
Como aplicar uma regra a uma base de dados?
```

Fluxo:

```text
CSV
 ↓
Pandas
 ↓
DataFrame
 ↓
Função
 ↓
if / elif / else
 ↓
apply()
 ↓
Nova informação
```

---

## Aula 04

A etapa seguinte é:

```text
Como automatizar tarefas e transformar dados em indicadores?
```

Fluxo:

```text
Dados
 ↓
Repetição
 ↓
Contagem
 ↓
Acumulação
 ↓
Cálculos
 ↓
Indicadores
 ↓
Interpretação
```

---

# 🛠 Tecnologias utilizadas

As aulas utilizam:

- **Python**
- **Google Colab**
- **Pandas**
- **Jupyter Notebook**
- Arquivos **CSV**

Principais recursos de Python trabalhados:

```python
True
False

if
elif
else

and
or
not

for
while
range()

listas
funções
contadores
acumuladores
```

Principais recursos do Pandas trabalhados:

```python
pd.read_csv()

df.head()

df.apply()

df.iterrows()

df.isna().sum()

df['coluna'].sum()

df['coluna'].mean()

df['coluna'].max()
```

---

# 🧠 Competências desenvolvidas

Ao longo da sequência, os estudantes praticam:

- Raciocínio lógico;
- Lógica booleana;
- Comparação de valores;
- Construção de regras condicionais;
- Tradução de regras de negócio para código;
- Criação de funções;
- Manipulação inicial de DataFrames;
- Leitura de arquivos CSV;
- Criação de novas colunas;
- Aplicação de funções em dados;
- Estruturas de repetição;
- Contadores e acumuladores;
- Verificação de valores ausentes;
- Cálculo de indicadores;
- Interpretação de resultados;
- Comunicação de resultados em linguagem de negócio.

---

# 📁 Arquivos

```text
├── Aula_Python02.ipynb
├── Aula_Python03.ipynb
└── Aula_Python04.ipynb
```

Durante as atividades, os notebooks também fazem referência aos seguintes arquivos de dados:

```text
alunos_desempenho.csv
pedidos_loja.csv
vendas_semana.csv
```

---

# 📌 Resumo da sequência

| Aula | Tema principal | Aplicação |
|---|---|---|
| Aula 02 | Booleanos, operadores e decisões | Classificação de risco de churn |
| Aula 03 | `if`, `elif`, `else`, funções e Pandas | Desempenho de alunos e regras de desconto |
| Aula 04 | Listas, `for`, `while`, contadores e acumuladores | Relatório semanal de vendas |

---

## 🎯 Resultado esperado

Ao final dessa sequência, o estudante já consegue compreender como utilizar estruturas fundamentais de Python para construir pequenas análises, aplicar regras a dados e produzir indicadores básicos a partir de arquivos CSV.

O projeto final conecta programação e análise de dados ao solicitar não apenas os cálculos, mas também a interpretação dos resultados em uma conclusão de negócio.
"""

path = Path("/mnt/data/README_Aulas_Python_02_03_04.md")
path.write_text(readme, encoding="utf-8")
print(f"Arquivo criado: {path}")
