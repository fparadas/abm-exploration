# 02 · Razão de partida dobrada e event sourcing

**Status:** proposto · **Fase:** 1 · **Ferramentas:** Julia, Arrow.jl/Parquet, DuckDB

## Pergunta

Dá para tornar a consistência stock-flow **estrutural** (impossível de violar) em vez de testada? E dá para reconstruir as duas matrizes do Godley e Lavoie como projeções de um log de eventos?

## Por que importa

No experimento 01, cada setor atualiza os próprios estoques, e nada impede um setor de criar dinheiro errando a conta. A partida dobrada remove essa possibilidade: setores só emitem fluxos com origem e destino; um único razão aplica cada fluxo debitando e creditando. A conservação vira um teorema sobre a matriz de incidência:

$$
u_{t+1} = u_t + B f_t, \qquad \mathbf{1}^\top B = 0 \;\Rightarrow\; \mathbf{1}^\top u_{t+1} = \mathbf{1}^\top u_t
$$

E se o estado é um fold do log, o log vira a fonte de verdade: novas projeções sem rodar a simulação de novo, diffs entre rodadas evento a evento.

## Modelo

O SIM do experimento 01, reescrito assim:

- `Fluxo(de, para, valor, tipo)` é o único tipo que setores produzem.
- `aplicar!(razao, fluxos)` é o único código que escreve estoques.
- Governo começa com saldo −H (moeda é passivo dele); a soma de todas as contas é zero sempre.

## Protocolo

1. Implementar `Fluxo`, `aplicar!` e os setores como funções que só devolvem `Vector{Fluxo}`.
2. Teste de propriedade: com setores que emitem fluxos **aleatórios**, a soma das contas continua zero após qualquer número de ticks. (Isso demonstra que a garantia independe do comportamento.)
3. **Gerar o razão a partir da fiação:** escrever uma função que lê o `WiringDiagram` do experimento 01, marca os fios monetários e produz B automaticamente. Comparar com o razão escrito à mão.
4. **Tick em três fases:** intenções → compensação → commit. No commit, checar factibilidade (saldo não negativo onde não há crédito) e rejeitar ou racionar.
5. **Event log:** gravar cada fluxo como evento (`run_id`, `periodo`, `de`, `para`, `valor`, `tipo`, `schema_version`) em Parquet; snapshot a cada N períodos.
6. **Projeções no DuckDB:** matriz de fluxos de um período (`GROUP BY de, para`) e balanço "as-of" t (soma assinada até t). Conferir com os estoques da simulação.
7. **Contas reais:** adicionar um estoque de bens com fonte (produção) e sumidouro (consumo) explícitos, como eventos próprios, e mostrar que a conservação estrita vale só para as contas financeiras.

## Critério de sucesso

- Teste de propriedade passa com comportamento arbitrário.
- B gerado da fiação coincide com o escrito à mão.
- Balanço e matriz de fluxos reconstruídos do log batem com a simulação.

## Armadilhas

- Factibilidade e gasto duplo não são garantidos pela partida dobrada; precisam do mercado (fase 2 do tick) e da checagem no commit.
- Reavaliações (ganho de capital) não são fluxos; ficam para depois.
- Versionar o esquema do evento desde o primeiro arquivo.

## Ideia de artigo

"Um funtor da fiação para a contabilidade": gerar automaticamente o razão consistente a partir do wiring diagram.

## Referências

- Godley e Lavoie (2007), matrizes de balanço, de fluxos e de reavaliação.
- Datomic/XTDB como alternativas de registro (ver [docs/03-projeto-pessoal.md](../docs/03-projeto-pessoal.md#registro-event-sourcing)).
