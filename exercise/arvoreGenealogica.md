# Árvore Genealógica de Personagens

**Disciplina:** AED1  
**Tema:** Funções Recursivas e Modularização  
 

---

## Contexto

Uma árvore genealógica cresce em profundidade arbitrária — pode ter 2 gerações ou 10. Funções iterativas com loops fixos não conseguem lidar com essa incerteza sem conhecer antecipadamente o tamanho da estrutura. A recursão resolve isso de forma natural: cada nó aplica a mesma lógica nos seus filhos, que aplicam nos seus netos, e assim por diante, até não haver mais descendentes.

Nesta atividade você irá representar a família de um personagem fictício usando dicionários aninhados e implementar funções recursivas para navegar, buscar e analisar essa estrutura.

O sistema deve ser dividido em **dois arquivos**:

- `utils.py` — contém todas as funções recursivas reutilizáveis
- `main.py` — contém os dados e a lógica principal que usa as funções

---

## Estrutura dos dados

Cada personagem é representado por um dicionário com três chaves:

```python
personagem = {
    "nome": "string",
    "idade": int,
    "filhos": []   # lista de dicionários com a mesma estrutura
}
```

Use a família abaixo como ponto de partida no seu `main.py`. Você pode adicionar mais personagens, mas deve manter ao menos **4 gerações** e **8 personagens**:

```python
familia = {
    "nome": "Aldo", "idade": 80, "filhos": [
        {"nome": "Beatriz", "idade": 55, "filhos": [
            {"nome": "Daniel",  "idade": 30, "filhos": []},
            {"nome": "Elisa",   "idade": 27, "filhos": [
                {"nome": "Hugo", "idade": 5, "filhos": []}
            ]}
        ]},
        {"nome": "Carlos",  "idade": 52, "filhos": [
            {"nome": "Fernanda", "idade": 25, "filhos": []},
            {"nome": "Gabriel",  "idade": 22, "filhos": []}
        ]},
        {"nome": "Diana",   "idade": 48, "filhos": [
            {"nome": "Isabela",  "idade": 20, "filhos": []}
        ]}
    ]
}
```

> **Importante:** não utilize listas ou dicionários globais adicionais para auxiliar as funções. Toda a informação necessária deve ser obtida navegando recursivamente pela estrutura acima.

---

## Parte 1 — `utils.py`

Implemente as seis funções abaixo. Cada uma exige uma abordagem recursiva diferente — leia atentamente o comportamento esperado antes de começar.

---

### `imprimir_arvore(no, nivel=0)`

Exibe a árvore completa com indentação proporcional à geração. Cada nível adiciona dois espaços de recuo.

**Comportamento esperado:**

```
Aldo (80 anos)
  Beatriz (55 anos)
    Daniel (30 anos)
    Elisa (27 anos)
      Hugo (5 anos)
  Carlos (52 anos)
    Fernanda (25 anos)
    Gabriel (22 anos)
  Diana (48 anos)
    Isabela (20 anos)
```

> Dica: o parâmetro `nivel` começa em 0 e é incrementado a cada chamada recursiva. Use `"  " * nivel` para gerar o recuo.

---

### `contar_descendentes(no)`

Retorna o número total de descendentes de um personagem (filhos, netos, bisnetos etc.). O próprio personagem não é contado.

**Caso base:** o personagem não tem filhos → retorna `0`.  
**Caso recursivo:** retorna a soma de `1` por cada filho mais o resultado de `contar_descendentes` aplicado a cada filho.

---

### `buscar_personagem(no, nome)`

Busca um personagem pelo nome em toda a árvore. Retorna o dicionário do personagem encontrado ou `None` se não existir.

**Caso base:** o nó atual tem o nome buscado → retorna o próprio nó.  
**Caso recursivo:** percorre os filhos recursivamente. Se algum retorno não for `None`, propaga esse resultado imediatamente.

> Atenção: a função deve interromper a busca assim que encontrar o personagem, sem continuar percorrendo os demais ramos.

---

### `calcular_geracao(no, nome, geracao=0)`

Retorna em qual geração o personagem se encontra. A raiz está na geração `0`, seus filhos na geração `1`, e assim por diante.

Retorna `-1` se o personagem não for encontrado.

---

### `listar_nomes(no)`

Retorna uma lista com os nomes de todos os personagens da árvore, na ordem em que são visitados (pré-ordem: pai antes dos filhos).

**Caso base:** o personagem não tem filhos → retorna uma lista com apenas o seu nome.  
**Caso recursivo:** concatena o nome atual com os resultados das chamadas recursivas em cada filho.

---

### `maior_idade(no)`

Percorre toda a árvore e retorna o dicionário do personagem mais velho.

**Caso base:** o personagem não tem filhos → retorna o próprio nó.  
**Caso recursivo:** compara a idade do nó atual com o mais velho retornado de cada sub-árvore e propaga o maior.

---

## Parte 2 — `main.py`

Com os dados definidos e as funções importadas de `utils.py`, estruture o `main.py` para executar as seguintes etapas em sequência:

1. **Exibir a árvore** completa usando `imprimir_arvore`.
2. **Solicitar um nome** ao usuário e usar `buscar_personagem` para localizar o personagem.
   - Se encontrado: exibir nome, idade, geração (via `calcular_geracao`) e número de descendentes (via `contar_descendentes`).
   - Se não encontrado: exibir mensagem adequada.
3. **Listar todos os membros** usando `listar_nomes`, exibindo os nomes separados por vírgula.
4. **Exibir o total de membros** da família (use `listar_nomes` para obter a lista e calcule o tamanho).
5. **Exibir o membro mais velho** usando `maior_idade`.
6. **Exibir os descendentes da raiz** usando `contar_descendentes` na raiz da árvore.

---

## Saída esperada

```
===== ÁRVORE GENEALÓGICA =====

Aldo (80 anos)
  Beatriz (55 anos)
    Daniel (30 anos)
    Elisa (27 anos)
      Hugo (5 anos)
  Carlos (52 anos)
    Fernanda (25 anos)
    Gabriel (22 anos)
  Diana (48 anos)
    Isabela (20 anos)

==============================

Digite o nome do personagem: Elisa

Personagem encontrado:
  Nome      : Elisa
  Idade     : 27 anos
  Geração   : 2
  Descendentes: 1

Todos os membros: Aldo, Beatriz, Daniel, Elisa, Hugo, Carlos, Fernanda, Gabriel, Diana, Isabela

Total de membros   : 10
Membro mais velho  : Aldo (80 anos)
Descendentes de Aldo: 9
```

---

## Por que cada função exige uma abordagem diferente?

| Função | Padrão recursivo | O que muda |
|---|---|---|
| `imprimir_arvore` | Parâmetro acumulado | O nível é passado adiante e aumentado a cada chamada |
| `contar_descendentes` | Soma de retornos | Cada chamada retorna um número que é somado ao nível acima |
| `buscar_personagem` | Retorno antecipado | A função para assim que encontra; caso contrário propaga `None` |
| `calcular_geracao` | Parâmetro + retorno antecipado | Combina os dois padrões anteriores |
| `listar_nomes` | Concatenação de listas | Cada chamada retorna uma lista que é somada (`+`) às demais |
| `maior_idade` | Comparação de retornos | Compara o nó atual com o melhor resultado das sub-árvores |

---

*Dúvidas? Utilize o fórum da disciplina ou o horário de atendimento.*
