# Atividade Prática — Sistema de Relatório de Vendas

**Disciplina:** AED1 
**Tema:** Funções e Modularização  
**Nível:** Intermediário  


---

## Contexto

Uma loja registra diariamente as vendas de 4 produtos ao longo de uma semana (7 dias). Você foi contratado para desenvolver um sistema em Python que processe esses dados e gere um relatório de desempenho com totais, médias e destaques da semana.

O sistema deve ser dividido em **dois arquivos**:

- `utils.py` — contém todas as funções auxiliares reutilizáveis
- `main.py` — contém os dados e a lógica principal que usa as funções

> **Por que dois arquivos?** As mesmas operações (total, média, maior, menor) precisam ser aplicadas em dois contextos diferentes: por produto e por dia. Centralizar essa lógica em `utils.py` evita repetição e torna o código mais organizado e fácil de manter.

---

## Dados de entrada

Utilize a estrutura abaixo como ponto de partida no seu `main.py`:

```python
produtos = ["Produto A", "Produto B", "Produto C", "Produto D"]

dias = ["Segunda", "Terça", "Quarta", "Quinta", "Sexta", "Sábado", "Domingo"]

# vendas[i][j] = unidades vendidas do produto i no dia j
vendas = [
    [45, 38, 52, 41, 60, 55, 21],  # Produto A
    [30, 42, 35, 48, 39, 55, 29],  # Produto B
    [28, 35, 40, 33, 45, 38, 22],  # Produto C
    [46, 47, 35, 40, 27, 53, 23],  # Produto D
]
```

---

## Parte 1 — `utils.py`

Implemente as funções a seguir. Cada uma deve ser **genérica**, recebendo apenas listas e parâmetros — sem conhecer os dados de vendas diretamente.

### Funções obrigatórias

```python
def calcular_total(valores):
    """Retorna a soma de uma lista de números."""
    pass

def calcular_media(valores):
    """Retorna a média aritmética de uma lista de números."""
    pass

def encontrar_maior(valores, nomes):
    """
    Recebe uma lista de valores e uma lista de nomes correspondentes.
    Retorna uma tupla (nome, valor) do maior elemento.
    """
    pass

def encontrar_menor(valores, nomes):
    """
    Recebe uma lista de valores e uma lista de nomes correspondentes.
    Retorna uma tupla (nome, valor) do menor elemento.
    """
    pass

def calcular_percentual(valor, total):
    """Retorna o percentual de valor em relação ao total, com 1 casa decimal."""
    pass

def formatar_linha(nome, total, media, percentual=None):
    """
    Retorna uma string formatada para o relatório.
    Se percentual for fornecido, inclui na linha.
    Exemplo: '  Produto A   | Total:  312 un | Média:  44.6 | 28.3%'
    """
    pass
```

> **Atenção:** não utilize variáveis globais nem importe os dados de `main.py` dentro de `utils.py`. As funções devem funcionar com qualquer lista passada como argumento.

---

## Parte 2 — `main.py`

Com os dados definidos e as funções importadas, estruture o `main.py` para:

1. **Importar** as funções de `utils.py`
2. **Calcular por produto** — para cada produto, calcular o total e a média de vendas nos 7 dias
3. **Calcular por dia** — para cada dia, calcular o total e a média de vendas dos 4 produtos
4. **Identificar destaques** — usar `encontrar_maior` e `encontrar_menor` tanto nos totais por produto quanto nos totais por dia
5. **Calcular participação** — usar `calcular_percentual` para mostrar a fatia de cada produto no total geral
6. **Exibir o relatório** — usar `formatar_linha` para compor todas as linhas de saída

---

## Saída esperada

O relatório gerado deve seguir o formato abaixo (os valores dependem da sua implementação):

```
===== RELATÓRIO DE VENDAS — SEMANA =====

--- Por produto ---
  Produto A   | Total:  312 un | Média:  44.6 | 28.3%
  Produto B   | Total:  278 un | Média:  39.7 | 25.2%
  Produto C   | Total:  241 un | Média:  34.4 | 21.9%
  Produto D   | Total:  271 un | Média:  38.7 | 24.6%

--- Por dia ---
  Segunda     | Total:  149 un | Média:  37.3
  Terça       | Total:  162 un | Média:  40.5
  Quarta      | Total:  162 un | Média:  40.5
  Quinta      | Total:  162 un | Média:  40.5
  Sexta       | Total:  171 un | Média:  42.8
  Sábado      | Total:  201 un | Média:  50.3
  Domingo     | Total:   95 un | Média:  23.8

-----------------------------------------
  Melhor produto : Produto A (312 un)
  Pior produto   : Produto C (241 un)
  Melhor dia     : Sábado   (201 un)
  Pior dia       : Domingo  ( 95 un)
```

---

## Critérios de avaliação

| Critério | Descrição | Peso |
|---|---|---|
| Correção funcional | As funções retornam os valores corretos para os dados fornecidos e para outros casos testados | 40% |
| Reutilização real | As funções de `utils.py` são chamadas mais de uma vez em `main.py`, sem duplicação de lógica | 25% |
| Clareza e nomes | Variáveis e funções com nomes descritivos; código legível | 20% |
| Relatório formatado | Saída alinhada e produzida via `formatar_linha`, sem formatações espalhadas pelo `main` | 15% |

---

## Extensões opcionais

Para quem concluir a atividade antes do prazo, as extensões abaixo valem pontos extras:

- **Classificação de desempenho:** implemente uma função `classificar_produto(total)` em `utils.py` que retorne `"alto"`, `"médio"` ou `"baixo"` com base em intervalos definidos. Exiba a classificação ao lado de cada produto no relatório.

- **Leitura de arquivo:** substitua os dados fixos por leitura de um arquivo `vendas.csv`, mantendo todas as funções de `utils.py` sem modificação.

- **Comparação de semanas:** receba os dados de duas semanas distintas e gere um relatório comparativo, reutilizando todas as funções já implementadas.

---

## Entrega

Envie os dois arquivos (`utils.py` e `main.py`) compactados em um `.zip` nomeado como `ra_nome_atividade2.zip`.  
Certifique-se de que o código executa sem erros antes de enviar.

---

*Dúvidas? Utilize o fórum da disciplina ou o horário de atendimento.*
