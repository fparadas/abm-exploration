# 04 · Mercados plugáveis e inteligência zero

**Status:** proposto · **Fase:** 4 · **Ferramentas:** Julia (despacho múltiplo), razão do experimento 02

## Pergunta

Com os agentes fixos, quanto do resultado de um mercado (eficiência alocativa, preços, distribuição) vem da **regra do mercado** e quanto vem do **comportamento** dos agentes?

## Por que importa

Regras de mercado são instituições, e muitas perguntas de política são sobre elas (teto de preço, prioridade no crédito, leilão vs preço fixo). Gode e Sunder (1993) mostraram que agentes de "inteligência zero", que só respeitam o próprio orçamento, atingem num leilão duplo eficiência próxima da de humanos. Reproduzir isso valida a arquitetura de mercados como caixas trocáveis.

## Modelo

- Interface única: `compensar(mecanismo, pedidos, oferta) -> Vector{Fluxo}`.
- Mecanismos: `Fila`, `Sorteio`, `Rateio`, `Tatonamento(sensibilidade)`, `LeilaoDuplo`.
- Agentes: compradores com valor de reserva e vendedores com custo, sorteados de distribuições fixas.
- Tipos de agente: **ZI-U** (lances aleatórios sem restrição), **ZI-C** (aleatórios com restrição orçamentária), e opcionalmente agentes que aprendem.

## Protocolo

1. Implementar a interface e os mecanismos; o razão do experimento 02 faz o commit.
2. Reproduzir Gode e Sunder: eficiência alocativa (excedente realizado / máximo) de ZI-U vs ZI-C no leilão duplo.
3. **Matriz agentes × mecanismos:** mesma população em todos os mecanismos; medir eficiência, dispersão de preço, quem fica racionado.
4. Adicionar uma restrição institucional no commit (teto de preço) e medir o efeito em cada mecanismo.
5. Decompor a variância dos resultados entre "mecanismo" e "tipo de agente".

## Critério de sucesso

- ZI-C no leilão duplo com eficiência alta (próxima dos valores reportados por Gode e Sunder), ZI-U bem abaixo.
- Trocar de mecanismo exige mudar um argumento, sem tocar em agentes ou razão.

## Armadilhas

- Conferir os valores numéricos do artigo original antes de declarar reprodução (citado de memória).
- Fila e sorteio dependem da ordem de chegada: fixar sementes e reportar média e dispersão.

## Referências

- Gode e Sunder (1993), "Allocative efficiency of markets with zero-intelligence traders", *Journal of Political Economy* (conferir).
- Arquitetura de mercados em [docs/03-projeto-pessoal.md](../docs/03-projeto-pessoal.md#mercados-instituições-e-economia-evolucionária).
