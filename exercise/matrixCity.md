cidade = [
    [1, 0, 2, 0, 1],
    [0, 9, 0, 1, 3],
    [1, 0, 1, 9, 2],
    [9, 3, 0, 0, 1],
    [0, 1, 2, 0, 9]
]
```

---

### 🎯 Missões

**Missão 1 — Relatório de danos**
Exiba o mapa formatado e conte quantas áreas de cada tipo existem na cidade.
```
=== MAPA DE NEXÓPOLIS ===
1 0 2 0 1
0 9 0 1 3
...

=== RELATÓRIO ===
Casas: X  |  Hospitais: X  |  Geradores: X  |  Áreas destruídas: X
```

---

**Missão 2 — Hospitais em perigo**
Um hospital está em perigo se tiver pelo menos uma **área destruída (`9`) entre seus 4 vizinhos** (cima, baixo, esquerda, direita).

Verifique cada hospital e exiba se está em situação de risco ou seguro.
```
Hospital em (0,2): SEGURO
Hospital em (2,4): EM PERIGO! Vizinho destruído detectado.
Hospital em (4,2): ...
```

> ⚠️ Atenção com os limites da matriz! Use `if` para garantir que o vizinho existe antes de acessá-lo.

---

**Missão 3 — Alcance do gerador**
Cada gerador (`3`) consegue fornecer energia para todos os quarteirões da **mesma linha** em que está.

Liste quais hospitais (`2`) serão atendidos por algum gerador. Um hospital é atendido se houver um gerador na mesma linha.
```
Gerador na linha 1 → Hospitais atendidos nessa linha: nenhum
Gerador na linha 3 → Hospitais atendidos nessa linha: (3, ?)
...
Total de hospitais com energia: X
```

---

**Missão 4 — Rota de evacuação 🌟 (bônus)**
Uma linha é uma **rota de evacuação segura** se não tiver nenhuma área destruída (`9`).

Exiba quais linhas são rotas seguras. Se nenhuma for segura, exiba um alerta geral.
```
=== ROTAS DE EVACUAÇÃO ===
Linha 0: SEGURA ✓
Linha 2: BLOQUEADA ✗
...
