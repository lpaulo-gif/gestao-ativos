# Estado do Projeto — Gestão de Ativos Financeiros Pessoais

## Etapas
- Etapa 1 — Levantamento de Requisitos: confirmada.
- Etapa 2 — Arquitetura de Software: confirmada.
- Etapa 3 — Modelagem do Banco de Dados: confirmada.
- Etapa 4 — Cadastro e Controle de Movimentações: confirmada.
- Etapa 5 — Motor de Cálculo de Rentabilidade: confirmada.
- Etapa 6 — Análise de Ativos Financeiros: confirmada.
- Etapa 7 — Atualização Automática de Dados: pendente de início.

## Decisões confirmadas
- Uso local, em computador, por um único usuário com autenticação.
- Escopo inicial: renda fixa e renda variável.
- Moeda-base: BRL; sem investimentos no exterior na V1.
- Cerca de cinco instituições.
- Movimentações: manual, CSV/extrato e estrutura preparada para automação futura.
- Orçamento inicial para infraestrutura e APIs: R$ 0.
- Método de custo para V1: custo médio ponderado móvel, com limitação fiscal documentada.
- Rentabilidade: TWR e MWR/IRR são métricas distintas; dados ausentes, estimados, atrasados ou inconsistentes devem ser sinalizados.
- Análise: separar vertentes fundamentalista, técnica e de risco; não gerar recomendação de compra/venda ou score único opaco.
- Indicadores analíticos devem exibir fonte, data de referência, fórmula/metodologia, benchmark quando aplicável, qualidade do dado e limitações.

## Próximo passo
Iniciar a Etapa 7 — Atualização Automática de Dados.

## Registro
Atualizado em 2026-09-27.
