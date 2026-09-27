# Estado do Projeto — Gestão de Ativos Financeiros Pessoais

## Etapas
- Etapa 1 — Levantamento de Requisitos: confirmada.
- Etapa 2 — Arquitetura de Software: confirmada.
- Etapa 3 — Modelagem do Banco de Dados: confirmada.
- Etapa 4 — Cadastro e Controle de Movimentações: confirmada.
- Etapa 5 — Motor de Cálculo de Rentabilidade: confirmada.
- Etapa 6 — Análise de Ativos Financeiros: proposta apresentada; aguardando confirmação.

## Decisões confirmadas
- Uso local, em computador, por um único usuário com autenticação.
- Escopo inicial: renda fixa e renda variável.
- Moeda-base: BRL; sem investimentos no exterior na V1.
- Cerca de cinco instituições.
- Movimentações: manual, CSV/extrato e estrutura preparada para automação futura.
- Orçamento inicial para infraestrutura e APIs: R$ 0.
- Método de custo para V1: custo médio ponderado móvel, com limitação fiscal documentada.
- Rentabilidade: TWR e MWR/IRR são métricas distintas; dados ausentes, estimados, atrasados ou inconsistentes devem ser sinalizados.

## Diretrizes propostas na Etapa 6
- Separar análises fundamentalista, técnica e de risco; não gerar score único ou recomendação de compra/venda.
- Calcular apenas indicadores cujos dados de origem e metodologia estejam documentados.
- Priorizar renda variável e renda fixa na V1; análise técnica fica opcional e isolada.
- Exibir sempre fonte, data de referência, benchmark, qualidade do dado e limitações do indicador.

## Próximo passo
Aguardar confirmação da Etapa 6 para iniciar a Etapa 7 — Atualização Automática de Dados.

## Registro
Atualizado em 2026-09-27.
