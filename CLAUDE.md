# CLAUDE.md

Contexto para continuar este trabalho no Claude Code. Leia isto primeiro; os detalhes estão em `docs/` e `experiments/`.

## Quem e o quê

- **Felipe Paradas**: engenheiro de software (Elixir/Phoenix, Gleam), mestrado em computação (UFRJ), bacharelado em CS (UnB) com base forte em cálculo, álgebra linear e econometria. Estuda economia; considera doutorado (CREST/IP Paris, IMPA, MADE-USP, UFRJ, Unicamp).
- **Objetivo do repositório:** um projeto pessoal que (1) implementa modelos macro de forma composicional em AlgebraicJulia, (2) serve de pretexto para estudar economia e (3) pode virar semente de pesquisa (doutorado).
- **Lente:** diálogo entre heterodoxia e ortodoxia. "Pensar com axiomas novos, provar com critérios compartilhados."
- **Idioma:** conversas e documentos em português brasileiro. Código e identificadores podem misturar português (domínio econômico: `familias`, `Fluxo`, `razao`) e inglês.

## O fio da conversa (resumo)

1. Teoria das categorias (CT) em economia: não gera teoremas econômicos novos; melhora a engenharia de modelos (composição, consistência, comparação). Torna modelos mais *verificáveis*, não mais *validáveis*. Vocação de meta-teoria.
2. Micro → macro: o paralelo certo é mecânica estatística → termodinâmica. A economia tem **feedback semântico** (agentes carregam modelos do sistema), o que gera pontos fixos em crenças, crítica de Lucas e limites computacionais (indecidibilidade só com agentes Turing-completos; caso típico é complexidade, PPAD).
3. Economia como "resultados locais rigorosos conectados por julgamento heurístico". Contínuo: identidades contábeis → regularidades robustas → regras de bolso.
4. ABMs: parte importante do futuro da macro, não o todo. Estocasticidade não resolve Lucas; aprendizado (fixar *como* se aprende) ajuda. Conectar ABMs exige identidade de agentes, escalas de tempo, consistência contábil e calibração conjunta.
5. Programa de pesquisa em três pilares (aprendizado, microdados, composição) e seis fases → `docs/01`. Avaliação franca: é agenda de laboratório; recorte factível = fase 2 como pesquisa, fase 1 mínima como projeto pessoal.
6. Projeto pessoal: SIM → PC → famílias heterogêneas → AB-SFC, em AlgebraicJulia. Lição de timing (saída depende do estado, não da entrada do mesmo período).
7. Consistência estrutural: **partida dobrada** (setores só emitem fluxos; um razão aplica) ⇒ conservação como teorema da matriz de incidência (1ᵀB = 0). Event sourcing: estado = fold do log; Parquet + DuckDB.
8. Tick em três fases: intenções → compensação (mercados, resolvem gasto duplo) → commit (factibilidade, regulação). Ativos financeiros se conservam; bens reais têm fontes/sumidouros.
9. Mercados plugáveis (despacho múltiplo), três níveis de regras (firma, interação, instituição externa), Gode-Sunder, instituições endógenas, economia evolucionária (Nelson e Winter).
10. ABM ≈ meta-heurística sem projetista. Objetivos num ABM (fora vs dentro do modelo). Governo como agente: composição de subagentes, Arrow, Kydland-Prescott.
11. **HANK como limite de uma subclasse de ABMs**: N → ∞ (propagação de caos/campo médio), aprendizado convergido (E-estabilidade/aproximação estocástica), fricção zero (pouco desenvolvido). CT dá a estrutura, **probabilidade dá os teoremas**, economia dá as perguntas. Mais expressivo não é melhor: HANK tem disciplina, análise e bem-estar definido. Mapa de domínios, não hierarquia.
12. "Quantos agentes são muitos": erro ≈ C/√N no caso bom; quebra com caudas pesadas (Gabaix, 1/ln N), interação forte e horizonte longo.

Felipe gostou especialmente do caminho de **matemática pesada** (probabilidade: propagação de caos, aproximação estocástica, grandes desvios) e da ideia de ponte entre escolas.

## Decisões tomadas

- Linguagem/stack inicial: **Julia + AlgebraicJulia** (aprender CT usando ferramenta pronta, antes de construir formalismo próprio).
- Tempo **discreto** por padrão (Godley e Lavoie é discreto); StockFlow.jl é contínuo, usar com adaptação se for o caso.
- Registro: começar com **Parquet + DuckDB**; banco imutável (XTDB preferível pela integração Postgres; Datomic pela elegância) só se necessário.
- Em cada etapa: implementar simples primeiro, depois composicional, e **medir o ganho real**. Se até a etapa 3 a composição não ajudar claramente, rebaixar CT a ferramenta.

## Próximos passos

1. Experimento 01: ler Godley e Lavoie cap. 3, montar as matrizes do SIM à mão, implementar o SIM em Julia puro como gabarito, depois a versão composicional.
2. Em paralelo, experimentos 05 (campo médio e N) e 06 (E-estabilidade), que não dependem de AlgebraicJulia.
3. Conferir as referências marcadas "de memória".
4. Estruturar melhor a trilha de estudo matemático: teoria da medida e processos estocásticos → propagação de caos e jogos de campo médio → aproximação estocástica.

## Convenções para o trabalho aqui

- Antes de usar uma API do AlgebraicJulia, conferir a documentação atual; o esboço em `docs/03` **não foi testado**.
- Toda simulação estocástica com semente explícita e várias sementes.
- Números citados em texto vêm de script, não de cópia manual.
- Experimentos ganham pasta própria (`experiments/NN-nome/`) quando tiverem código; o `.md` evolui para relatório.
- Distinguir sempre o que é fato conferido, o que é citação de memória e o que é especulação.
- Projeto relacionado (não misturar): **Murmur**, biblioteca pessoal de ABM em Gleam/OTP.

## Documentos de origem

Os três documentos em `docs/` foram exportados de Claude Docs (claude.ai) em 12 nov. 2026. Os diagramas que eram widgets foram redesenhados em Mermaid.
