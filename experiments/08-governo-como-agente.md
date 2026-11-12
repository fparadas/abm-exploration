# 08 · Governo como agente

**Status:** proposto · **Fase:** 5 (em miniatura) · **Ferramentas:** SIM/PC composicional (01), agentes que aprendem (06)

## Pergunta

Num modelo pequeno com agentes que aprendem, compare quatro formas de representar o governo: **otimizador único**, **regra fixa**, **agente que aprende** e **composição de subagentes** (banco central e Tesouro com objetivos próprios). Quando a escolha muda as conclusões?

## Por que importa

- Tratar o governo como um único otimizador esconde problemas: ele é uma composição de subagentes (escolha pública), "o objetivo do governo" pode nem ser bem definido (Arrow), e otimizar com discrição pode sair pior que seguir regra (inconsistência temporal de Kydland e Prescott).
- Também testa as duas formas de pôr um objetivo num ABM: **fora** (otimizar a política por cima da simulação) e **dentro** (planejador que age enquanto os agentes reagem).
- É a composição categórica de novo: o governo é uma caixa que, aberta, tem um diagrama dentro.

## Modelo

- Base: SIM ou PC com famílias que aprendem a expectativa de inflação ou de renda (mínimos quadrados, como no experimento 06).
- Governo:
  1. **Regra fixa:** G e θ constantes, ou regra de Taylor nos juros (no PC).
  2. **Otimizador fora do modelo:** busca (bayesiana ou genética) dos parâmetros da regra que minimizam uma perda (volatilidade de Y, desvio de inflação), sob várias sementes.
  3. **Discrição:** reotimiza a cada período tomando as expectativas como dadas.
  4. **Subagentes:** banco central (perda de inflação) e Tesouro (perda de produto/dívida), compostos como duas caixas.

## Protocolo

1. Implementar as quatro versões com a mesma fiação externa.
2. Medir perda média, volatilidade e caminhos de expectativa.
3. Mostrar o viés inflacionário da discrição quando agentes aprendem a antecipar o governo.
4. Com a versão "fora do modelo", checar **reward hacking**: a política ótima explora algum artefato do modelo? Avaliar robustez sobre a distribuição de parâmetros.
5. Tratar como multiobjetivo: traçar a fronteira de Pareto entre crescimento/estabilidade/distribuição em vez de uma perda única.

## Critério de sucesso

- Um caso em que regra fixa supera discrição por causa do aprendizado dos agentes.
- Um caso em que a composição de subagentes gera dinâmica que o otimizador único não gera (por exemplo, conflito fiscal-monetário).

## Armadilhas

- Otimizar contra o comportamento atual dos agentes reabre Goodhart/Lucas: a avaliação tem que deixar os agentes se adaptarem.
- O objetivo é uma escolha normativa; reportar trade-offs, não "a política ótima".

## Referências

- Kydland e Prescott (1977), "Rules rather than discretion".
- Buchanan e Tullock (1962), *The Calculus of Consent*; Arrow (1951), *Social Choice and Individual Values*.
- Zheng et al., "The AI Economist" (Salesforce), planejador aprendendo por reforço.
(De memória; conferir.)
