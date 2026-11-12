# 07 · Instituições endógenas

**Status:** proposto · **Fase:** 4 · **Ferramentas:** mercados plugáveis do experimento 04

## Pergunta

Se cada firma escolhe a própria regra de venda (fila, rateio, sorteio, preço que reage ao estoque) e pode trocá-la por **imitação** ou **busca local** quando vai mal, a população de firmas converge para as regras "boas"? As regras do mercado deixam de ser parâmetro e viram resultado da simulação?

## Por que importa

É a economia evolucionária de Nelson e Winter em miniatura: rotinas como genes, busca como mutação, mercado como seleção. Testa se a arquitetura com mecanismos como objetos trocáveis dá conta de instituições endógenas, e conecta com path dependence e lock-in.

## Modelo

- M firmas, cada uma com `mecanismo::Mecanismo` e um preço.
- Consumidores com busca simples (visitam k firmas, compram na mais barata com estoque; ou ficam fiéis com probabilidade φ).
- Seleção: lucro por período; firmas abaixo de um limiar trocam de regra com probabilidade p, imitando uma firma melhor (exploração) ou testando uma regra vizinha (busca local). Firmas com prejuízo persistente saem e entram firmas novas.

## Protocolo

1. Rodar com distribuição inicial uniforme de regras; acompanhar as participações ao longo do tempo.
2. Variar a busca dos consumidores (k, φ): a regra vencedora muda?
3. Variar a taxa de exploração: medir convergência prematura (lock-in numa regra pior) vs diversidade persistente (exploration vs exploitation, James March).
4. Choque institucional: impor um teto de preço no meio da simulação e ver a reorganização das regras.
5. Comparar o resultado evolutivo com o que um "planejador" escolheria (a regra de maior excedente total do experimento 04).

## Critério de sucesso

- Identificar condições em que a seleção encontra a regra eficiente e condições em que trava numa ineficiente.

## Armadilhas

- Seleção depende de frequência: a melhor regra depende das regras das outras. Não procurar um ótimo fixo.
- Separar o efeito da regra do efeito do preço (controle: todas as firmas com o mesmo preço).

## Referências

- Nelson e Winter (1982), *An Evolutionary Theory of Economic Change*.
- March (1991), "Exploration and exploitation in organizational learning".
- Arthur (1989), retornos crescentes e lock-in.
(De memória; conferir.)
