# 🌩️ Desafio: O Apagão de MatrixCity

## 📖 História

Uma tempestade devastou a cidade de **MatrixCity**. Várias áreas foram destruídas e os hospitais estão sem energia. Felizmente, a cidade possui geradores de emergência espalhados pelos quarteirões.

Você é o **coordenador de crise** e precisa analisar o mapa da cidade para tomar decisões rápidas. Cada quarteirão da grade é representado por um número:

| Valor | Significado |
|-------|-------------|
| `0`   | Rua vazia |
| `1`   | Casa residencial 🏠 |
| `2`   | Hospital 🏥 |
| `3`   | Gerador de emergência ⚡ |
| `9`   | Área destruída 💥 |

---

## 🗺️ Mapa da cidade

```python
cidade = [
    [1, 0, 2, 0, 1],
    [0, 9, 0, 1, 3],
    [1, 0, 1, 9, 2],
    [9, 3, 0, 0, 1],
    [0, 1, 2, 0, 9]
]
```

---

## 🎯 Missões

### Missão 1 — Relatório de danos

Exiba o mapa formatado e conte quantas áreas de cada tipo existem na cidade.

**Saída esperada:**
```
=== MAPA DE MatrixCity ===
1 0 2 0 1
0 9 0 1 3
1 0 1 9 2
9 3 0 0 1
0 1 2 0 9

=== RELATÓRIO ===
Casas: X  |  Hospitais: X  |  Geradores: X  |  Áreas destruídas: X
```

---

### Missão 2 — Hospitais em perigo

Um hospital está em perigo se tiver pelo menos uma **área destruída (`9`)** entre seus 4 vizinhos (cima, baixo, esquerda, direita).

Verifique cada hospital e exiba se está em situação de risco ou seguro.

**Saída esperada:**
```
Hospital em (0,2): SEGURO
Hospital em (2,4): EM PERIGO! Vizinho destruído detectado.
Hospital em (4,2): ...
```

> ⚠️ Atenção com os limites da matriz! Use `if` para garantir que o vizinho existe antes de acessá-lo.

---

### Missão 3 — Alcance do gerador

Cada gerador (`3`) consegue fornecer energia para todos os quarteirões da **mesma linha** em que está.

Liste quais hospitais (`2`) serão atendidos por algum gerador. Um hospital é atendido se houver um gerador na mesma linha.

**Saída esperada:**
```
Gerador na linha 1 → Hospitais atendidos nessa linha: nenhum
Gerador na linha 3 → Hospitais atendidos nessa linha: (3, ?)
...
Total de hospitais com energia: X
```

---

### Missão 4 — Rota de evacuação 🌟 (bônus)

Uma linha é uma **rota de evacuação segura** se não tiver nenhuma área destruída (`9`).

Exiba quais linhas são rotas seguras. Se nenhuma for segura, exiba um alerta geral.

**Saída esperada:**
```
=== ROTAS DE EVACUAÇÃO ===
Linha 0: SEGURA ✓
Linha 1: BLOQUEADA ✗
Linha 2: BLOQUEADA ✗
Linha 3: SEGURA ✓
Linha 4: BLOQUEADA ✗
```

---

## 🔧 Dicas

- **Missão 1:** use `for` aninhado para percorrer linhas e colunas; para exibir sem colchetes, use `print(cidade[i][j], end=" ")` e `print()` ao final de cada linha.
- **Missão 2:** use `if i > 0:` antes de checar `cidade[i-1][j]`, e `if i < len(cidade)-1:` antes de checar `cidade[i+1][j]`. O mesmo vale para as colunas.
- **Missão 3:** para cada linha, percorra as colunas duas vezes — uma buscando geradores, outra buscando hospitais.
- **Missão 4:** use uma variável `segura = True` e defina como `False` se encontrar um `9` na linha.
