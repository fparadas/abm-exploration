# 06 · E-estabilidade na teia de aranha

**Status:** proposto · **Fase:** 2 → 3 (trilha matemática) · **Ferramentas:** Julia puro

## Pergunta

Agentes que aprendem por mínimos quadrados recursivos convergem para as expectativas racionais? A teoria diz: sim se e só se o equilíbrio for **E-estável**. E com **ganho constante**, o que acontece em vez de convergência?

## Por que importa

É o segundo limite da ponte ABM → HANK (aprendizado convergido). Mostra concretamente: (1) na região E-estável, o modelo racional é a boa aproximação; (2) na região instável, o equilíbrio racional existe mas ninguém o alcança; (3) com ganho constante surgem flutuações e fugas raras, que são probabilidade de alto nível (grandes desvios) com história econômica concreta.

## Modelo

Teia de aranha: pₜ = μ + α·Eₜ₋₁pₜ + ηₜ.

- Lei percebida: pₜ = a + ruído. Lei efetiva: média T(a) = μ + αa.
- Equilíbrio racional: a\* = μ/(1 − α). E-estável ⇔ α < 1.
- Aprendizado: aₜ = aₜ₋₁ + γₜ (pₜ − aₜ₋₁).
  - ganho decrescente: γₜ = 1/t;
  - ganho constante: γₜ = γ.
- EDO associada: da/dτ = T(a) − a = μ − (1 − α)a.

## Protocolo

1. Simular com γₜ = 1/t para α ∈ {−0,5; 0,5; 0,9; 1,1}; várias sementes. Mostrar convergência quase certa para α < 1 e divergência para α > 1.
2. Sobrepor a solução da EDO (no tempo τ = Σγₜ) às trajetórias: o método da EDO de Ljung em ação.
3. Ganho constante: simular para vários γ; mostrar a distribuição estacionária de aₜ (≈ normal com variância de ordem γ) e medir a frequência de grandes desvios em função de γ.
4. (Extensão) Modelo com dois equilíbrios racionais (por exemplo, inflação de senhoriagem com dois estados estacionários): mostrar que o aprendizado seleciona o E-estável e que, com ganho constante, há fugas ocasionais (Sargent).
5. (Extensão) Heterogeneidade: N agentes com ganhos diferentes; comparar com o caso homogêneo.

## Critério de sucesso

- Fronteira α = 1 reproduzida numericamente.
- Trajetórias acompanhando a EDO.
- Escala da variância com γ conferida.

## Armadilhas

- Para α próximo de 1, a convergência é lentíssima: não confundir com divergência; usar horizonte longo.
- Para α < −1 no ganho constante, cuidado com oscilações numéricas (γ grande).

## Leitura

- Evans e Honkapohja (2001), *Learning and Expectations in Macroeconomics*.
- Borkar, *Stochastic Approximation: A Dynamical Systems Viewpoint* (entrada leve na matemática).
- Kushner e Yin, *Stochastic Approximation and Recursive Algorithms and Applications* (referência completa).
- Sargent (1999), *The Conquest of American Inflation*.
(De memória; conferir edições.)
