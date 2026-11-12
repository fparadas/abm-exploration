# 03 · Famílias heterogêneas e agregação

**Status:** proposto · **Fase:** 1 → 3 · **Ferramentas:** Julia, a arquitetura dos experimentos 01 e 02

## Pergunta

Se trocarmos a caixa "famílias" por várias famílias heterogêneas (por exemplo, poupadoras e gastadoras) com as mesmas portas, **quando a soma delas se comporta exatamente como uma família agregada**, e quando não? Em linguagem categórica: quando o mapa "heterogêneo → agregado" é um funtor (comuta com a dinâmica)?

## Por que importa

É a versão em miniatura da pergunta "quando o agente representativo é legítimo?", o coração da ponte entre ortodoxia e heterodoxia e o germe da fase 3.

## Modelo

- K tipos de família com propensões (α1ᵏ, α2ᵏ) e pesos de renda sᵏ, mesma interface do SIM (entra W·N e ΔH; sai C e T).
- Caixa "Soma" agrega C e T.
- Família agregada candidata com (ᾱ1, ᾱ2) = médias ponderadas.

## Protocolo

1. **Caso linear.** Com regras de consumo lineares e participação de renda fixa, derivar à mão as condições para que agregar e simular comute com simular e agregar. (Esperado: comuta se a distribuição de riqueza entre tipos for constante ou se α2ᵏ for igual entre tipos.)
2. **Verificação numérica.** Rodar ambas as versões e medir a distância entre trajetórias de Y e H.
3. **Quebrar a agregação** de três jeitos e medir o erro:
   - α2 diferente entre tipos (a distribuição de riqueza importa);
   - não linearidade (restrição de liquidez: consumo ≤ H);
   - transições de tipo estocásticas (como em Carvalho e Di Guilmi; Grasselli e Li).
4. **Mapa de suficiência.** Para cada quebra, tabelar quando o erro do agregado é desprezível e quando não é.
5. Ligar com o experimento 05: com muitas famílias e tipos estocásticos, o agregado converge para uma equação de campo médio?

## Critério de sucesso

- Condição analítica de comutação para o caso linear, conferida numericamente.
- Um diagnóstico operacional: "dado este módulo, o agregado é suficiente se e somente se ...".

## Armadilhas

- Igualar trajetórias só no estado estacionário esconde diferenças de dinâmica; comparar as transições.
- A versão heterogênea pode precisar de mais estado; documentar o que a família agregada "esquece".

## Referências

- Carvalho e Di Guilmi, SFC com agentes heterogêneos e agregação via mecânica estatística ([slides](https://av.fields.utoronto.ca/programs/scientific/13-14/newthinking/Corrado_Di_Guilmi.pdf)).
- Grasselli e Li (2018), [master equation approach](https://www.math.mcmaster.ca/~grasselli/Grasselli_Li_2017_accepted_JNTF.pdf).
- Sonnenschein-Mantel-Debreu (contexto do resultado negativo geral).
