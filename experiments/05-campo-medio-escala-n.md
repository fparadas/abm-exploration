# 05 · Campo médio e escala de N

**Status:** proposto · **Fase:** 3 (trilha matemática) · **Ferramentas:** Julia puro (ou Python); depois probabilidade no papel

## Pergunta

Num ABM simples com limite de campo médio conhecido, **como o erro entre o agregado simulado e o limite cai com o número de agentes N**? Quando a taxa é 1/√N, e quando ela quebra (caudas pesadas, interação forte)?

## Por que importa

O primeiro dos três limites que levam de ABMs ao HANK (N → ∞) é uma lei dos grandes números para agentes que interagem: **propagação de caos**. Este experimento é o "resultado de brinquedo" que liga simulação e teorema: a simulação gera a conjectura (inclinação no log-log), a probabilidade tenta prová-la. E responde à pergunta prática "quantos agentes são muitos?".

## Modelo base (famílias com choques de renda)

- N famílias; renda yᵢₜ = ȳ·exp(σ εᵢₜ), εᵢₜ i.i.d.
- Regra de poupança: aᵢ,ₜ₊₁ = (1 + r)(aᵢₜ + yᵢₜ − cᵢₜ), com cᵢₜ = κ (aᵢₜ + yᵢₜ), aᵢₜ ≥ 0.
- **Interação via campo médio:** r depende da riqueza média, rₜ = r(āₜ) (por exemplo, decrescente em ā).
- Limite: a distribuição μₜ de riqueza evolui por uma equação determinística (operador de transição com r(∫a dμₜ)).

## Protocolo

1. Escrever o limite de campo médio e resolvê-lo numericamente (histograma ou discretização da distribuição).
2. Rodar o ABM com N ∈ {10³, 10⁴, 10⁵, 10⁶}, ≥ 50 sementes cada.
3. Medir o erro de ā e de alguns quantis contra o limite; fazer o gráfico log-log do erro contra N.
4. **Regime bem comportado:** esperar inclinação ≈ −1/2. Comparar o C empírico com o coeficiente de variação.
5. **Quebras:**
   - caudas pesadas: substituir os choques (ou, num segundo modelo, o tamanho de firmas) por Pareto/Zipf; verificar a convergência mais lenta (no caso de Zipf para firmas, Gabaix sugere 1/ln N);
   - interação forte: r muito sensível a ā (próximo de bifurcação);
   - horizonte: como o erro cresce com T para N fixo.
6. Tentar escrever o esboço de prova de propagação de caos para o caso bem comportado (acoplamento com cópias independentes do processo de McKean-Vlasov).

## Critério de sucesso

- Gráfico log-log com inclinação ≈ −1/2 no caso base e inclinação mais rasa nas quebras.
- Uma tabela "N necessário para erro de 1%" por variável.
- Uma conjectura enunciada com precisão (e, se possível, provada).

## Conta de referência

Erro ≈ C/√N ⇒ N ≈ (C/ε)². Para ε = 1%: C ≈ 1 → N ≈ 10 mil; C ≈ 4 → N ≈ 160 mil.

## Armadilhas

- Separar o erro de discretização do limite do erro de N finito.
- Com caudas pesadas, médias amostrais entre sementes também convergem devagar: usar medianas e intervalos robustos.

## Referências

- Sznitman, "Topics in propagation of chaos" (Saint-Flour); Kac.
- Achdou, Han, Lasry, Lions e Moll, HANK em tempo contínuo como jogo de campo médio; Cardaliaguet, Delarue, Lasry e Lions, *The master equation and the convergence problem in mean field games*.
- Gabaix (2011), "The granular origins of aggregate fluctuations", Econometrica.
- Duffie e Sun, lei dos grandes números exata para um contínuo de agentes.
(Todas de memória; conferir.)
