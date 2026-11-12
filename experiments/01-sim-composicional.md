# 01 · SIM composicional

**Status:** proposto · **Fase:** 1 · **Ferramentas:** Julia, Catlab.jl, AlgebraicDynamics.jl (talvez StockFlow.jl)

## Pergunta

A composição de setores (famílias, firmas, governo) como caixas num wiring diagram, via `oapply`, reproduz **número por número** o modelo SIM de Godley e Lavoie escrito à mão? E o que a composição obriga a explicitar que a versão à mão esconde?

## Por que importa

É o critério de passagem da fase 1 e o teste mais barato do pilar de teoria das categorias. Também é o pretexto para estudar contabilidade nacional: matriz de balanço, matriz de fluxos de transações e a regra "todo fluxo sai de algum lugar e entra em outro".

## Modelo

SIM (Godley e Lavoie, *Monetary Economics*, cap. 3): economia fechada, só moeda do governo como ativo.

- Produção: Y = C + G
- Renda disponível: YD = W·N − T, com W·N = Y
- Impostos: T = θ·W·N
- Consumo: C = α1·YD + α2·H_{t−1}
- Moeda: ΔH = G − T (governo) e ΔH = YD − C (famílias)
- Parâmetros de referência: θ = 0,2; α1 = 0,6; α2 = 0,4; G = 20
- Estado estacionário: Y\* = G/θ = 100

## Protocolo

1. **À mão.** Montar as matrizes de balanço e de fluxos do SIM no papel antes de qualquer código.
2. **Gabarito.** Implementar o SIM em Julia puro (resolvendo a simultaneidade algebricamente dentro do período). Guardar a trajetória como fixture.
3. **Versão composicional.** Escrever a fiação (sintaxe) e as `DiscreteMachine`s (semântica) separadamente; compor com `oapply`. Esboço em [docs/03-projeto-pessoal.md](../docs/03-projeto-pessoal.md#esboço-em-algebraicjulia).
4. **Timing.** No AlgebraicDynamics a saída de uma máquina depende só do estado, não da entrada do mesmo período. Implementar a convenção "paga agora o que decidiu antes" e comparar:
   - (a) estado estacionário com o gabarito (deve bater exatamente);
   - (b) trajetória de transição (vai diferir; quantificar);
   - (c) uma versão com renda esperada no estilo do SIMEX.
5. **Diagrama.** Gerar `to_graphviz` da fiação e versionar a imagem.
6. **Troca de caixa.** Substituir as famílias por outra máquina com as mesmas portas (por exemplo, α1 diferente) sem tocar no diagrama. Registrar quantas linhas mudaram em cada versão (à mão vs composicional).

## Critério de sucesso

- Estado estacionário idêntico ao gabarito (tolerância numérica de máquina).
- Invariante H_famílias + M_firmas = Hs_governo verdadeira em todos os períodos.
- Uma nota curta sobre o que a composição obrigou a decidir (timing, quem observa o quê).

## Armadilhas

- API do AlgebraicDynamics pode ter mudado: conferir a documentação atual antes (o esboço não foi testado).
- StockFlow.jl é em tempo contínuo; SIM é discreto. Se usar StockFlow, documentar a adaptação de semântica.
- Não confundir diferença de transição (esperada, por causa do timing) com erro de implementação: o teste forte é o estado estacionário e o invariante.

## Referências

- Godley e Lavoie (2007), *Monetary Economics*, cap. 3 (SIM e SIMEX).
- [AlgebraicDynamics.jl, API](https://algebraicjulia.github.io/AlgebraicDynamics.jl/dev/api); [exemplo ciberfísico](https://algebraicjulia.github.io/AlgebraicDynamics.jl/stable/examples/Cyber-Physical).
- Baez et al., [Compositional modeling with stock and flow diagrams](https://arxiv.org/abs/2205.08373v3).
