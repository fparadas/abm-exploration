# Caderno de exploração: economia, computação e categorias

5 nov. 2026 (atualizado em 12 nov. 2026) · Felipe Paradas

Notas abertas que acompanham o [programa de pesquisa](01-programa-de-pesquisa.md) sobre ABMs composicionais. Aqui ficam as ideias soltas, analogias e dúvidas; o plano formal fica no outro documento.

## Teoria das categorias e economia

**Ideia central:** CT não gera teoremas econômicos novos; ela melhora a engenharia de modelos. O ganho é composição, consistência e comparação.

- **Composicionalidade.** Agentes e setores como sistemas abertos com interfaces tipadas, colados com garantia de que a composição é bem definida.
- **Sintaxe separada da semântica.** O mesmo diagrama vira ODE agregada, processo estocástico ou ABM. Dá pra comparar a versão representativa com a heterogênea a partir da mesma especificação.
- **Consistência por construção.** Fluxos sem contrapartida não tipam (StockFlow.jl).
- **ABM como reescrita de grafos.** Estado como C-set, regras declarativas (AlgebraicJulia).

**Verificar não é validar.** CT torna o modelo mais *verificável* (ele faz o que especifiquei?), mas não mais *validável* (o que especifiquei descreve a economia?). Ajuda com testes por partes, invariantes por construção, leis como property-based tests e oráculos cruzados entre semânticas (ABM com N grande converge pra versão agregada?).

**CT como meta-teoria.** É a vocação natural dela: "matemática sobre matemática". Na economia, serviria para:

- tornar o conhecimento cumulativo, com modelos como componentes reutilizáveis;
- mapear a teoria (o que é caso particular de quê, onde escolas realmente divergem);
- formalizar a ponte micro-macro;
- aproximar o modelo do paper do código da simulação.

Por que não aconteceu: custo de entrada alto, incentivo acadêmico premia resultado novo e não infraestrutura. Um problema de bem público.

## Micro → macro e autorreferência

**Analogia certa:** o paralelo não é quântica→clássica, é mecânica estatística→termodinâmica. Muitas partículas, poucas variáveis macro.

- **Parecido:** ambos perdem informação ao agregar. A física resolveu bem (lei dos grandes números, renormalização). A economia tem o resultado negativo de Sonnenschein-Mantel-Debreu: a estrutura micro quase não restringe o macro.
- **Pior na economia:** partículas não leem jornal (crítica de Lucas), não há leis de conservação fortes, e a interação não é fraca nem aleatória (redes, imitação, bolhas).
- **Ponte com CT:** coarse-graining como funtor. "Essa agregação preserva estrutura?" vira "isso é um funtor?".

**Feedback semântico.** Física tem feedback dinâmico (o spin responde ao campo médio). Economia tem feedback *semântico*: agentes carregam modelos do sistema do qual fazem parte. O loop é estado → crenças → ações → estado. Consequências:

- equilíbrio vira ponto fixo em crenças (expectativas racionais; Grunberg e Modigliani, 1954);
- as regras do loop mudam, porque agentes aprendem;
- aparecem limites computacionais.

**Computabilidade, com precisão.** Autorreferência sozinha não implica Turing-completude. A cadeia é: agentes capazes de rodar programas arbitrários (Turing-completo) + autorreferência → indecidibilidade (linha de Velupillai e Alain Lewis). Modelos padrão restringem agentes de propósito, e aí o problema vira complexidade: equilíbrio de Nash é PPAD-completo (Daskalakis, Goldberg e Papadimitriou).

**O que "economia é indecidível" quer dizer.** Não existe algoritmo geral que responda toda pergunta sobre todo sistema econômico. Não impede responder casos específicos nem prever estatisticamente. A física tem o mesmo (spectral gap indecidível; Cubitt, Pérez-García e Wolf, 2015). Uma economia real é finita, então o problema prático é intratabilidade. Lição: não existe *o* modelo; existem classes restritas de modelos.

**E a praxeologia?** Não quebra. Gödel não torna falsas deduções válidas; só impede a pretensão de completude. Em parte reforça Mises e Hayek: limites computacionais formalizam o problema do cálculo e do conhecimento contra o planejador central. Mas valem igualmente contra o teórico de qualquer escola. As críticas mais fortes à praxeologia estão em outro lugar: o status do axioma da ação, hipóteses empíricas escondidas e o alcance das conclusões de política.

## Natureza do conhecimento econômico

**Formulação de trabalho:** economia é uma ciência de resultados locais rigorosos, conectados por julgamento heurístico sobre quando cada um se aplica. O rigor está nas peças; a heurística, na escolha e na composição delas.

**Dois sentidos de heurística:**

- Os modelos são heurísticas: uma biblioteca de modelos, cada um válido em certas condições (Rodrik, *Economics Rules*).
- Os agentes usam heurísticas: racionalidade limitada e satisficing (Simon); heurísticas simples às vezes superam otimização sob incerteza (Gigerenzer).

**A macro é mais heurística que a micro.** Okun, Phillips e Taylor são regularidades ou regras de bolso instáveis. Motivos: poucos dados independentes, problema de agregação e crítica de Lucas. DSGE tentou escapar com microfundamentos, mas o agente representativo é ele mesmo uma heurística.

**Um contínuo, não uma dicotomia:**

| Tipo | Exemplo | Status |
| --- | --- | --- |
| Identidade contábil | Poupança = investimento | Verdade por definição |
| Regularidade robusta | Hiperinflação e financiamento monetário de déficits | Indutiva, mas com mecanismo, robusta entre contextos e resistente à crítica de Lucas |
| Regra de bolso | Lei de Okun, curva de Phillips | Instável, muda com contexto e política |

Toda ciência empírica é indutiva (Hume). Se "padrão consistente" bastasse para chamar algo de heurística, a física inteira seria heurística. O critério útil é mecanismo + robustez + resistência à crítica de Lucas.

**Crenças como estado.** O sistema econômico é dinâmico e seu estado inclui crenças. Mas nem toda atualização vem de crença (choques reais, estoques lentos) e nem toda mudança de crença propaga (fricções filtram). Às vezes crença sozinha basta: corrida bancária em Diamond-Dybvig, equilíbrios múltiplos. O canal principal são os preços, que agregam crenças dispersas (Hayek).

## ABMs

**São o futuro da macro?** Parte importante dele, não o todo.

- **A favor:** heterogeneidade real, redes, não linearidades e crises endógenas; uso institucional (Banco da Inglaterra no mercado imobiliário); previsão competitiva com VAR e DSGE (Poledna e coautores, 2023); microdados e computação viabilizam milhões de agentes.
- **Contra:** calibração e validação fracas; regras ad hoc reabrem a crítica de Lucas (o "deserto da racionalidade limitada" de Sims); opacidade; HANK absorvendo a demanda por heterogeneidade dentro do mainstream.
- **Aposta:** cenário plural. ABMs onde redes e crises importam (estabilidade financeira, habitação, cadeias produtivas); HANK/DSGE fortes em política monetária; híbridos com agentes que aprendem e microdados.

**Estocasticidade não resolve Lucas.** O problema não é determinismo, é parâmetro que muda com a política. Uma regra estocástica com distribuição fixa continua fixa. O que ajuda é subir um nível: fixar *como* o agente aprende, não *o que* ele faz, e estimar usando variação de regime.

**Conectar ABMs é possível, mas não é só plugar.** Os problemas:

- **Identidade dos agentes:** a família do módulo imobiliário é a mesma do módulo de crédito? Se não for, perde-se o feedback que justificou o ABM.
- **Escalas de tempo:** dias no financeiro, meses no imobiliário, anos no capital.
- **Consistência contábil:** dinheiro que sai de um módulo precisa entrar em outro.
- **Calibração conjunta:** módulos calibrados isoladamente não formam um sistema calibrado.

A engenharia já faz co-simulação (padrão FMI). É o caso de uso mais concreto de CT no programa.

## Analogias termodinâmicas

**Ajuste na intuição inicial:** começar uma indústria costuma ser mais caro por unidade do que expandir (custos fixos, depois economias de escala). O que tem cara de termodinâmica é que a expansão vem em saltos, não de forma suave.

| Física | Economia | Referência |
| --- | --- | --- |
| Energia de ativação | Custo fixo e barreira de entrada; política industrial como catalisador | — |
| Calor latente | Investimento em blocos: produção parada até a planta nova ficar pronta | Literatura de *lumpy investment* |
| Histerese | Firmas entram com preço alto e não saem quando ele volta; desemprego que persiste | Dixit; Blanchard e Summers |
| Inércia | Path dependence e lock-in com retornos crescentes | Brian Arthur; Paul David (QWERTY) |
| Entropia | Produção como processo irreversível, com limite físico ao crescimento | Georgescu-Roegen |

**Cuidado:** Mirowski (*More Heat than Light*) mostrou que a economia neoclássica copiou a física do século XIX quase literalmente. A analogia falha porque energia se conserva e valor não, e porque partículas não formam crenças. Serve como fonte de intuições estruturais, não como equação importada.

**Gancho para ABMs:** saltos e histerese são fáceis de modelar com agentes (custos irreversíveis, capacidade discreta) e difíceis em modelos representativos suaves.

## Calibração de ABMs versus treino com Adam

**Ideia central:** numa rede neural o parâmetro é só um meio para prever; num ABM o parâmetro é a teoria, porque o contrafactual depende do valor exato dele.

**Grupos de parâmetros num ABM macro:**

- **Comportamentais:** propensão a consumir, taxa de aprendizado, memória, intensidade de troca de heurística. Estimados indiretamente.
- **De mecanismo:** velocidade de ajuste de preços, fricções de matching, reação do crédito à inadimplência. Estimados indiretamente.
- **Institucionais:** alíquotas, limites de LTV, regra do banco central. Lidos da legislação.
- **Condições iniciais e distribuições:** renda, riqueza, firmas, redes. Lidos de microdados.
- **Choques:** volatilidade e persistência. Estimados ou calibrados.

| | Rede neural com Adam | ABM |
| --- | --- | --- |
| Número de parâmetros | Milhões a bilhões | Dezenas |
| Gradiente | Exato, via backpropagation | Em geral não existe |
| Custo de avaliar a perda | Barato, um minibatch | Caro, uma simulação inteira |
| Ruído na perda | Amostragem dos dados | A própria simulação |
| Dados | Muitos exemplos independentes | Uma única história |
| O que importa | A previsão | O valor de cada parâmetro |
| Objetivo | Um ponto ótimo | Uma posterior, com incerteza |

**Identificação** é o problema que a rede neural não tem: várias combinações de parâmetros podem reproduzir os mesmos dados e dar contrafactuais diferentes.

**Métodos:**

- **Momentos simulados:** distância entre estatísticas simuladas e reais, minimizada sem gradiente (Nelder-Mead, genéticos, otimização bayesiana).
- **Inferência baseada em simulação:** uma rede neural aprende a mapear dados → posterior dos parâmetros. O Adam volta aqui, um nível acima: treina a rede que inverte o ABM.
- **Emuladores:** uma rede imita o ABM; calibra-se no emulador com gradiente e confere-se no original.
- **ABMs diferenciáveis:** relaxações suaves das decisões discretas para permitir backpropagation direto. Fronteira, com gradientes ruidosos.

**Ponte com CT:** num ABM diferenciável, cada agente vira literalmente uma lens parametrizada. Calibrar e treinar passam a ser a mesma operação.

**Cuidado de vocabulário:** algoritmos genéticos podem aparecer como *mecanismo de aprendizado dentro* do modelo (agentes evoluem) ou como *otimizador de fora* para calibrar. Não misturar os dois.

## Objetivos, governo e a ponte ABM → HANK

**ABM e meta-heurísticas.** Mesmo maquinário (populações, regras locais, aleatoriedade, emergência). Meta-heurística é um ABM com objetivo imposto pelo projetista; ABM é uma meta-heurística sem projetista. Conceitos atravessam a fronteira: exploration vs exploitation (James March nas organizações), convergência prematura como lock-in, busca local como a "busca" de Nelson e Winter. No ABM evolucionário, a população remodela a paisagem de fitness enquanto sobe nela (mercado artificial do Santa Fe, de Arthur e Holland; Arifovic com algoritmos genéticos em macro).

**Pôr um objetivo num ABM.** Dois jeitos:

- **Fora do modelo:** o ABM é o simulador e um otimizador procura a política (alíquota, regra de juros) que maximiza o objetivo.
- **Dentro do modelo:** um agente planejador age enquanto os outros reagem e aprendem (AI Economist).

Cuidados: Goodhart e Lucas (agentes se adaptam à política), "reward hacking" do modelo, robustez sobre sementes e sobre a posterior da calibração, e o objetivo como escolha normativa. Melhor olhar a fronteira de Pareto entre crescimento, estabilidade e distribuição.

**O governo como agente otimizador.** Útil como referência, mas com três ressalvas: o governo é uma composição de subagentes com objetivos próprios (escolha pública; e o teorema de Arrow diz que "o objetivo do governo" pode nem ser bem definido); otimizar com discricionariedade pode sair pior que seguir regra (inconsistência temporal de Kydland e Prescott); e na prática governos seguem heurísticas (regra de Taylor). No ABM: otimizador único, regras fixas, agente que aprende ou composição de subagentes (banco central e Tesouro como caixas dentro de uma caixa).

**HANK como limite de ABMs.** A afirmação defensável não é "HANK é só uma redução", e sim "HANK é o limite de uma subclasse de ABMs, sob condições específicas". São três limites compostos:

| Limite | O que acontece | Matemática que já existe |
| --- | --- | --- |
| N → ∞ | Agentes finitos viram uma distribuição | Jogos de campo médio e master equation (Achdou, Han, Lasry, Lions, Moll; Cardaliaguet e coautores) |
| Aprendizado convergido | Regras viram políticas ótimas; expectativas viram racionais | E-estabilidade (Evans e Honkapohja), aproximação estocástica |
| Fricção zero | Matching descentralizado vira equilíbrio walrasiano | Pouco desenvolvido; provavelmente o mais difícil |

O que se perde no limite: flutuações de tamanho finito, efeitos de rede, dinâmica fora do equilíbrio, bolhas de aprendizado. O resultado útil seria: "nestas condições, HANK é a aproximação correta; fora delas, isto é o que ele deixa de ver".

**Expressividade não é virtude por si só.** A inclusão não é total: HANK representa equilíbrios E-*instáveis*, que nenhum agente que aprende alcança. E a relação é de aproximação no limite, não de igualdade. Mais importante: como numa linguagem com tipos restritos versus uma Turing-completa, o modelo mais restrito permite provar mais. O HANK tem disciplina (poucos graus de liberdade), intuição analítica e bem-estar bem definido (utilidade dos otimizadores). Formulação: **HANK é o regime de um ABM em que o aprendizado convergiu, os mercados não têm fricção e há muitos agentes; dentro desse regime é a ferramenta melhor; fora dele, o ABM vê coisas que o HANK não vê.** Mapa de domínios, não hierarquia.

**Por que a probabilidade é o que mais conta.** A passagem é uma lei dos grandes números para agentes que interagem e aprendem:

- N → ∞ é **propagação de caos** (Kac, Sznitman): agentes ficam assintoticamente independentes, cada um interagindo só com a distribuição média.
- Aprendizado convergindo é **aproximação estocástica** (Robbins-Monro, método da EDO de Ljung).
- A probabilidade dá **taxas** (ruído da ordem de 1/√N): com quantos agentes o HANK já é boa aproximação?
- E diz **quando falha**: com caudas pesadas no tamanho das firmas, os choques individuais não se cancelam (hipótese granular de Gabaix, 2011).
- Até o "contínuo de agentes independentes" do HANK é delicado: Judd apontou o problema, Duffie e Sun construíram uma lei dos grandes números exata para resolvê-lo.

**Divisão do trabalho:** a CT dá a estrutura (quais mapas compõem a redução e o que cada um preserva), a probabilidade dá os teoremas (quando, com que velocidade, quando falha), a economia dá as perguntas (o que se perde importa para política?).

## Aprendizado e E-estabilidade

Agentes como econometristas: acreditam numa lei de movimento com parâmetro β (lei *percebida*); agindo com base nela, geram uma lei *efetiva* T(β). Expectativas racionais são o ponto fixo β\* = T(β\*).

Com mínimos quadrados recursivos e ganho decrescente (γ_t = 1/t), a recursão β_t = β_{t−1} + γ_t (erro de previsão) se comporta como a EDO dβ/dτ = T(β) − β. O equilíbrio é **E-estável** quando essa EDO é estável (caso linear: autovalores de DT(β\*) com parte real < 1). Sob regularidade, o aprendizado converge quase certamente para os E-estáveis (Evans e Honkapohja).

- **Exemplo mínimo (teia de aranha):** p_t = μ + α E_{t−1} p_t + ruído. Com previsão constante a, T(a) = μ + αa, equilíbrio a\* = μ/(1−α), E-estável sse α < 1.
- **Seleção de equilíbrios:** com múltiplos equilíbrios racionais, o aprendizado escolhe os E-estáveis.
- **Ganho constante** (mais realista): sem convergência a um ponto; crenças flutuam e fazem raras **fugas**, analisadas com teoria de grandes desvios (Sargent, *The Conquest of American Inflation*).
- **Limites:** resultados clássicos supõem agentes homogêneos e modelo bem especificado; com modelos errados surgem equilíbrios de percepção restrita; aprendizado por reforço multiagente é bem mais difícil.
- **Leitura:** Evans e Honkapohja (2001); Borkar, *Stochastic Approximation: A Dynamical Systems Viewpoint*; Kushner e Yin.

## Quantos agentes são "muitos"?

Depende da variável, do erro tolerado e da interação. No caso bem comportado (variância finita, interação fraca): erro ≈ C/√N, logo N ≈ (C/ε)², com C ≈ coeficiente de variação.

- Erro de 1%, C ≈ 1 (renda): N ≈ 10 mil. C ≈ 4 (riqueza): N ≈ 160 mil.
- **Caudas pesadas:** com Zipf (tamanho de firmas, Gabaix), a volatilidade agregada cai só como 1/ln N. Com 1 milhão de firmas, ln N ≈ 14: "muitos" pode nunca bastar.
- **Interação forte** (hubs, manada, transições de fase) aumenta o C efetivo.
- **Horizonte longo:** limites de propagação de caos costumam crescer exponencialmente com o tempo.
- **Na economia real N é fixo:** famílias provavelmente estão no regime bem comportado; firmas e principalmente bancos (setor concentrado), provavelmente não.

Ver o experimento [05-campo-medio-escala-n](../experiments/05-campo-medio-escala-n.md).

## Perguntas em aberto

- [ ] Dá para definir uma noção formal de "agregação legítima" que seja testável com microdados?
- [ ] Regras de aprendizado são de fato mais estáveis entre regimes do que regras de comportamento? Que evidência existe?
- [ ] Qual é a menor classe de agentes que já torna um ABM Turing-completo? E isso importa na prática?
- [ ] Histerese e investimento em blocos mudam a resposta de um ABM a choques de juros de forma relevante para política?
- [ ] ABMs diferenciáveis valem o esforço, ou inferência baseada em simulação já resolve a calibração?
- [ ] Existe algum resultado econômico que só fica visível quando o modelo é composto, e não em nenhum módulo isolado?
- [ ] O terceiro limite (fricção zero → equilíbrio walrasiano) pode ser formalizado como um limite probabilístico de mecanismos de matching?

*Referências deste caderno vêm de memória, exceto as já conferidas no programa de pesquisa. Conferir antes de uso formal.*
