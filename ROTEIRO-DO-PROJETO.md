# ROTEIRO DO PROJETO — Gestão de Ativos Financeiros Pessoais

> Pré-requisito: as Regras Globais (G1–G9), o contexto/convenções do projeto e o modo de operação recomendado neste ambiente estão em `AGENTS.md`, lido automaticamente no início da sessão. Este arquivo contém o roteiro etapa a etapa do desenvolvimento — siga a ordem e respeite a G5 (pare e aguarde confirmação ao final de cada etapa).
>
> **Persistência:** salve este arquivo na raiz do repositório (não apenas como mensagem de chat). A G6 do `AGENTS.md` instrui a relê-lo no início de toda sessão — é o que permite retomar o projeto numa sessão nova sem repassar as etapas manualmente.
>
> **Ordem de leitura:** (1) "Primeira Resposta Esperada" abaixo — o que fazer na sua primeiríssima resposta neste projeto; (2) "Formato de Entrega" — o padrão a seguir do meio ao fim do projeto; (3) as 11 etapas, em ordem, a partir da Etapa 1.

---

## Primeira Resposta Esperada

Se esta é a primeira mensagem deste projeto (ainda não existe `docs/ESTADO_DO_PROJETO.md`, ou ele indica que nada foi confirmado), sua primeira resposta deve apresentar **apenas**:

1. Um resumo do sistema proposto.
2. Os principais módulos sugeridos (incluindo o módulo de Análise de Ativos, Etapa 6).
3. As decisões técnicas que precisam ser tomadas.
4. **Somente as perguntas obrigatórias** da Etapa 1, subseção 1.1 (G7) — não as importantes/opcionais ainda.
5. Uma proposta provisória de MVP, marcada explicitamente como "sujeita a revisão após as respostas".
6. O plano da Versão 1 (Etapa 11), em linhas gerais.

Não apresente implementação completa antes de concluir o diagnóstico inicial e obter minha confirmação (G5, G8).

Se `docs/ESTADO_DO_PROJETO.md` já existir com etapas confirmadas (retomando uma sessão anterior), pule esta seção: leia o arquivo (G6) e continue da etapa em que o projeto parou, sem repetir o diagnóstico inicial.

---

## Formato de Entrega (para toda etapa, a partir da Etapa 1)

1. Objetivo da etapa.
2. Requisitos.
3. Premissas (rotuladas como tal — G2).
4. Proposta técnica.
5. Entregáveis.
6. Dependências.
7. Riscos.
8. Critérios de aceitação.
9. **Atualização de `docs/ESTADO_DO_PROJETO.md`** (G6).

Quando fornecer código: indique nome e finalidade de cada arquivo, dependências, como executar, como testar, sem omitir trechos essenciais. Não declare a aplicação "pronta" sem demonstrar o que foi de fato implementado e testado neste ambiente (G1/G2/G3). Informe explicitamente qualquer limitação de execução, integração ou acesso a dados externos — inclusive bloqueios de sandbox/rede (AGENTS.md, Seção 4).

---

## Etapa 1 — Levantamento de Requisitos

Antes de qualquer arquitetura ou código, diagnostique o projeto. Aplique G7: apresente primeiro só as perguntas **obrigatórias**.

### 1.1. Perguntas obrigatórias (fazer primeiro)
1. O sistema será usado por apenas um usuário? Precisa de login/autenticação?
2. Acesso será por celular, computador, ou ambos? Uso local ou hospedado na internet?
3. Quais classes de ativos entram na primeira versão?
4. Quantas instituições/contas de investimento serão cadastradas, aproximadamente?
5. Há investimentos no exterior ou em moedas diferentes de BRL?
6. Como as movimentações históricas serão inseridas (manual, importação de CSV/extrato)?
7. Qual é o orçamento disponível para hospedagem, banco de dados e APIs?

### 1.2. Perguntas importantes (fazer depois das obrigatórias)
- Preferência de stack tecnológica? Nível de conhecimento em programação/infraestrutura?
- Rentabilidade diária, mensal, anual, acumulada? Comparação com índices de referência?
- Separar valorização de mercado dos rendimentos recebidos? Considerar taxas/impostos?
- Frequência de atualização de preços desejada?
- Necessidade de automação de cotações, proventos, importação de corretoras?
- Para o módulo de análise de ativos (Etapa 6): quais classes têm prioridade para análise (ações, FIIs, renda fixa, cripto)? Há preferência por análise fundamentalista, técnica, de risco, ou as três? Existe algum benchmark de referência preferido (ex.: CDI, Ibovespa, IPCA+)?

### 1.3. Perguntas opcionais (versões futuras)
- Alertas de sincronização, exportação de relatórios, múltiplos perfis, etc.

### 1.4. Entregável da etapa
Após as respostas às perguntas obrigatórias, apresente: requisitos funcionais, requisitos não funcionais, premissas adotadas, restrições técnicas, dependências externas e recursos adiados para versões futuras. Finalize atualizando `docs/ESTADO_DO_PROJETO.md` (G6) e aguarde confirmação (G5) antes de seguir para a Etapa 2.

---

## Etapa 2 — Arquitetura de Software

Com base nos requisitos fechados na Etapa 1, proponha a arquitetura.

**Componentes a avaliar:** interface web responsiva, backend com API, banco de dados, autenticação, módulo de movimentações, motor de rentabilidade, serviço de atualização de dados, importação de arquivos, logs/monitoramento, backup/recuperação. Explique finalidade e dependências de cada um.

**Escolha tecnológica:** sugira stack considerando manutenção, custo, segurança, bibliotecas disponíveis, integração com fontes financeiras, facilidade de deploy e escalabilidade compatível com uso pessoal (ver G9 para comparações).

**Entregáveis:** diagrama de arquitetura (Mermaid, conforme convenção 3.5 do AGENTS.md), descrição dos componentes, fluxo de dados, tecnologias propostas, estrutura de diretórios, estratégia de configuração, requisitos de implantação, riscos e limitações técnicas.

Finalize atualizando `docs/ESTADO_DO_PROJETO.md` (G6) e aguarde confirmação (G5).

---

## Etapa 3 — Modelagem do Banco de Dados

Projete um modelo normalizado.

**Entidades a avaliar:**
- *Usuário/config:* usuário, preferências, moedas, parâmetros de cálculo.
- *Instituições e ativos:* instituição, conta, ativo, classe de ativo, mercado/país, moeda do ativo.
- *Movimentações:* compra, venda, aporte, resgate, transferência, taxas, impostos, ajustes, eventos corporativos.
- *Dados de mercado:* cotação, data/hora de referência, fonte, histórico, status de atualização, qualidade do dado.
- *Rendimentos:* proventos, juros, dividendos, distribuições, data de referência/pagamento, valor, ativo de origem.
- *Indicadores de análise (ver Etapa 6):* indicador calculado, ativo/classe de referência, fórmula/metodologia utilizada, valor, data de cálculo, benchmark usado (quando aplicável), fonte de dado de origem. Necessário para a tela de "análise de ativos" da Etapa 8 ter o que exibir — sem essa entidade, os indicadores da Etapa 6 não têm onde ser persistidos.

Para cada entidade especifique: nome, finalidade, campos, tipos, identificador, relacionamentos, restrições de integridade, regras de validação e exemplo de registro. Evite duplicidade e preserve histórico (não altere registros históricos destrutivamente sem estratégia de auditoria — ver G1/G2). Diferencie dados inseridos manualmente de dados obtidos por fontes externas.

**Entregáveis:** modelo entidade-relacionamento, dicionário de dados, esquema do banco, exemplos de registro, regras de integridade, estratégia de migrações futuras.

Finalize atualizando `docs/ESTADO_DO_PROJETO.md` (G6) e aguarde confirmação (G5).

---

## Etapa 4 — Cadastro e Controle de Movimentações

**Funcionalidades:** cadastrar, editar (respeitando integridade), cancelar/corrigir, consultar histórico, filtrar por ativo/instituição/período, importar arquivos, identificar duplicados, validar campos obrigatórios, registrar origem e data de inclusão.

**Campos mínimos:** data da operação, data de liquidação, instituição, conta, ativo, tipo de operação, quantidade, preço unitário, valor bruto, taxas, impostos, valor líquido, moeda, referência externa, observações.

**Regras de negócio:** defina explicitamente para compras, vendas parciais/totais, aportes, resgates, transferências, taxas, proventos, ajustes e eventos corporativos — como cada operação afeta saldo de quantidade, custo de aquisição, fluxo de caixa e rentabilidade. **Não presuma** método de custo médio ou tratamento fiscal sem documentar metodologia e limitações (G1/G2).

Finalize atualizando `docs/ESTADO_DO_PROJETO.md` (G6) e aguarde confirmação (G5).

---

## Etapa 5 — Motor de Cálculo de Rentabilidade

Módulo central do sistema.

**Indicadores a avaliar:** valor total da carteira, valor por instituição/classe/ativo, total de aportes e resgates, rendimentos recebidos, custos e taxas, resultado de valorização, rentabilidade por período e acumulada, evolução patrimonial, contribuição de cada ativo ao resultado.

**Metodologias obrigatórias a especificar:**
- **TWR (Time-Weighted Return):** explique o método, como isolar o efeito dos fluxos externos de capital, tratamento de subperíodos.
- **MWR/IRR (Money-Weighted Return):** explique aplicação quando o momento/valor dos aportes e resgates importa para o resultado do investidor; dados de entrada e limitações.
- **Rentabilidade por ativo e classe:** considerando compras, vendas, fluxos, proventos, custos, mudanças de quantidade e dados de mercado.

Nunca apresente um único percentual como se representasse todos os objetivos de análise (G4).

**Regras de precisão a documentar:** convenção de datas, tratamento de feriados/dias sem cotação, precisão decimal (retomando convenção 3.5 do AGENTS.md), moeda de referência, dados ausentes, cotações atrasadas, valores estimados, tratamento de erros, arredondamento na apresentação. Use exemplos numéricos para validar. Se uma métrica não puder ser calculada com confiabilidade para alguma classe, informe a limitação em vez de apresentar resultado enganoso (G1).

Finalize atualizando `docs/ESTADO_DO_PROJETO.md` (G6) e aguarde confirmação (G5).

---

## Etapa 6 — Análise de Ativos Financeiros

**Objetivo.** Enquanto o Motor de Rentabilidade (Etapa 5) mede o *desempenho passado* da carteira, este módulo avalia a *qualidade, o risco e o valuation* dos ativos, individualmente ou por classe, usando modelos e boas práticas reconhecidos no mercado. Reforça G4: em nenhuma hipótese os resultados aqui devem ser apresentados como recomendação de compra/venda — são insumos de análise para decisão do próprio usuário.

### 6.1. Modelos por classe de ativo

**Ações — análise fundamentalista:**
- Indicadores de valuation: P/L, P/VP, EV/EBITDA, Dividend Yield, ROE, ROIC, margem líquida, dívida líquida/EBITDA, CAGR de receita e lucro.
- Modelos de precificação: Fluxo de Caixa Descontado (DCF), Modelo de Desconto de Dividendos (Gordon), múltiplos comparáveis (peer/sector comparison).
- Análise técnica (tratar como módulo **opcional e claramente separado** do fundamentalista, sinalizando seu valor preditivo limitado): médias móveis, RSI, MACD, suporte/resistência.

**FIIs:** P/VP, dividend yield, vacância física e financeira, cap rate, tipo de fundo (tijolo, papel, híbrido, fundo de fundos), qualidade/concentração de inquilinos e contratos, liquidez em bolsa.

**Renda fixa:** yield to maturity, duration, marcação a mercado vs. curva de referência, rating de crédito do emissor, spread sobre benchmark (CDI, Selic, IPCA), risco de liquidez e de crédito.

**Criptoativos:** volatilidade histórica, correlação com outros ativos/classes, liquidez de mercado, métricas on-chain quando disponíveis — com ressalva explícita sobre a limitação de modelos tradicionais de valuation para essa classe.

**Investimentos no exterior:** mesmos princípios fundamentalistas ajustados à moeda e ao mercado local, com destaque para a exposição cambial como fator de risco separado.

### 6.2. Indicadores de risco (transversais a todas as classes)
Volatilidade (desvio-padrão dos retornos), Índice de Sharpe, Índice de Sortino, máximo drawdown, beta em relação a um benchmark, correlação entre ativos/classes (para análise de diversificação), Value at Risk (VaR) quando aplicável — sempre com ressalva das limitações do modelo.

### 6.3. Boas práticas específicas desta etapa
- Separar claramente análise fundamentalista, técnica e de risco — nunca combiná-las em um "score único" sem explicitar a metodologia por trás (G2/G4).
- Basear todo indicador em fonte de dado documentada (ver Etapa 7 — Atualização de Dados); **nunca calcular ou estimar um múltiplo quando o dado de origem não estiver disponível** — sinalizar a ausência em vez de inventar (G1).
- Indicar sempre o benchmark/comparável usado em cada análise.
- Sinalizar explicitamente quando um modelo não é adequado à classe do ativo (ex.: DCF tem aplicação limitada a FIIs de papel; análise técnica tem valor preditivo debatido academicamente).
- Expor o racional/fórmula por trás de cada indicador ao usuário, mantendo a transparência de cálculo definida na missão do projeto (AGENTS.md, Seção 1).

### 6.4. Entregáveis da etapa
1. Catálogo de indicadores/modelos por classe de ativo, com fórmula e fonte de dado necessária para cada um.
2. Regras de exibição: quando o dado de origem não existir, não calcular o indicador e sinalizar a ausência ao usuário.
3. Estrutura de tela/relatório de análise (a integrar com a Etapa 8 — Dashboard).
4. Lista de limitações conhecidas de cada modelo, redigida para ser exibida ao usuário junto do indicador (não apenas em documentação interna).

Finalize atualizando `docs/ESTADO_DO_PROJETO.md` (G6) e aguarde confirmação (G5).

---

## Etapa 7 — Atualização Automática de Dados

> **Nota operacional:** esta etapa depende de acesso à rede para consultar fontes externas. Siga o Modo de Operação Recomendado (AGENTS.md, Seção 4) — nunca simule uma resposta de API para contornar a ausência de rede no sandbox (G1); sinalize a necessidade de `network_access = true` ou aprovação manual e aguarde autorização antes de prosseguir.

**Fontes a avaliar** (ações, FIIs, fundos, renda fixa, cripto, moedas, proventos, dados históricos — inclui as fontes que alimentam os indicadores da Etapa 6): para cada uma, documentar dados disponibilizados, cobertura, frequência, limitações de acesso, custo, termos de uso, disponibilidade da API, risco de indisponibilidade e necessidade de validação manual. **Não invente endpoints ou credenciais** (G1).

**Rotina de sincronização:** agendamento, identificação dos ativos, consulta à fonte, validação da resposta, armazenamento, registro de origem, tratamento de falhas, logs, reprocessamento, notificação de erro.

**Segurança:** nunca solicitar/armazenar senhas de corretoras em texto aberto; não recomendar automação de acesso a contas protegidas sem avaliar autorização, segurança e compatibilidade técnica.

Finalize atualizando `docs/ESTADO_DO_PROJETO.md` (G6) e aguarde confirmação (G5).

---

## Etapa 8 — Dashboard e Interface Web

**Tela principal (conforme dados disponíveis):** patrimônio total, variação do período, rentabilidade acumulada e por período, total de proventos, distribuição da carteira, última atualização, alertas de falhas/dados pendentes. Nunca apresente indicadores como atualizados quando os dados subjacentes estiverem desatualizados (G1/G2).

**Telas a avaliar:** dashboard, carteira consolidada, ativos, movimentações, proventos, instituições, histórico de rentabilidade, análise por classe, **análise de ativos (indicadores fundamentalistas, técnicos e de risco — ver Etapa 6)**, importação, configurações, status das integrações.

**Gráficos a especificar** (com fonte de dados, filtros, unidade e período para cada um): evolução do patrimônio e da rentabilidade, distribuição por classe/instituição, contribuição de ativos, proventos ao longo do tempo, aportes e resgates, **comparação de indicadores fundamentalistas/de risco entre ativos ou frente a um benchmark (Etapa 6)**.

Finalize atualizando `docs/ESTADO_DO_PROJETO.md` (G6) e aguarde confirmação (G5).

---

## Etapa 9 — Segurança e Proteção dos Dados

Considere: autenticação, autorização, gestão de sessão, proteção de credenciais, criptografia em trânsito, armazenamento seguro de segredos, validação de entradas, proteção contra vulnerabilidades comuns, logs sem exposição de dados sensíveis, backup, recuperação, controle de acesso à produção.

Se houver dados pessoais, avalie requisitos de privacidade/LGPD aplicáveis ao ambiente de implantação. **Não presuma conformidade legal automática** — identifique o que precisa de avaliação específica (G1).

Finalize atualizando `docs/ESTADO_DO_PROJETO.md` (G6) e aguarde confirmação (G5).

---

## Etapa 10 — Testes e Validação

> **Nota operacional:** os testes de integração que dependem de fontes externas (ver Etapa 7) seguem o Modo de Operação Recomendado do AGENTS.md quanto a acesso à rede — não finja um resultado de teste bloqueado por falta de rede como se fosse um resultado obtido (G1/G3).

**Testes unitários:** compra, venda, preço médio (se aplicável), aportes, resgates, proventos, custos, rentabilidade, conversão de moedas, **cálculo de indicadores de análise (Etapa 6) com valores de entrada conhecidos**.

**Testes de integração:** banco de dados, importação de movimentações, atualização de cotações, processamento de proventos, consistência entre módulos, tratamento de erros de API.

**Cenários com dados fictícios** (compra, compra adicional, venda parcial, provento, aporte posterior, resgate parcial, alteração de cotação, falha de atualização, duplicidade, período sem cotação): para cada um, informe dados de entrada, operações, resultado esperado, resultado obtido **apenas se o código foi de fato executado**, e critério de aprovação (G3).

Finalize atualizando `docs/ESTADO_DO_PROJETO.md` (G6) e aguarde confirmação (G5).

---

## Etapa 11 — Plano de Desenvolvimento

Desenvolvimento incremental. **Aplique G5 rigorosamente aqui:** cada versão abaixo só começa após eu confirmar a anterior.

- **V1 — Fundação:** requisitos, arquitetura, banco de dados, autenticação (se necessária), cadastro de ativos/instituições, cadastro básico de movimentações.
- **V2 — Consolidação:** cálculo de posições, consolidação da carteira, controle de proventos, relatórios básicos, validação de saldos.
- **V3 — Rentabilidade e Análise:** motor de rentabilidade, histórico patrimonial, indicadores por ativo/classe/período, gráficos de evolução, testes numéricos abrangentes, **módulo de análise de ativos (Etapa 6): catálogo inicial de indicadores fundamentalistas e de risco por classe, com fórmula e fonte documentadas**.
- **V4 — Automação:** integração com fontes de dados, atualização programada, logs de sincronização, tratamento de falhas, conferência de dados, importação de arquivos, **atualização automática dos dados que alimentam os indicadores de análise (ex.: balanços, indicadores de mercado)**.
- **V5 — Aprimoramentos:** UX/UI, alertas, exportação, performance, backup/recuperação, novas classes de ativos, **expansão do módulo de análise (ex.: análise técnica opcional, novos modelos de valuation)**.

**Como este plano se relaciona com as Etapas 1 a 10:** as Etapas 1 a 10 são a especificação completa do sistema — o que cada módulo deve fazer, com quais regras e dados. A implementação em código, porém, não segue a ordem das etapas; segue o faseamento V1 a V5 acima, que recombina pedaços de várias etapas em cada entrega. Depois que este plano for confirmado (G5), o próximo trabalho é construir cada versão, uma de cada vez: apresente e implemente a V1, aplicando o Formato de Entrega e parando para confirmação (G5); só então siga para a V2; e assim por diante até a V5. Só pergunte quais são os próximos passos depois que a V5 estiver de fato implementada e testada neste ambiente — não apenas planejada.

Finalize atualizando `docs/ESTADO_DO_PROJETO.md` (G6) e aguarde confirmação (G5) — isso encerra a etapa de planejamento (a apresentação deste plano). A implementação de V1 a V5 é o trabalho seguinte, conforme o parágrafo acima.
