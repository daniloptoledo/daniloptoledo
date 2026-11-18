# Danilo Portilho

Estudante de **Engenharia da Computação no UNISAL** (conclusão prevista para dez/2028), em Campinas, SP. Assistente Operacional na ProAventura desde set/2026, acompanhando a operação de e-commerce no Mercado Livre e na Amazon, do pedido à expedição.

Meu foco é **automação e dados**: pegar um problema real (de uma empresa, da minha família, da minha comunidade) e transformar em um sistema que as pessoas usam de verdade.

**Resultados em uso real:**
- **Catálogo B2B (ProAventura):** cotação para revendedor de **mais de 1 hora para 10 a 15 minutos**.
- **Chamada da Crisma:** registrar a presença de um encontro de **10 a 15 minutos para 2 minutos**.
- **Financeiro Familiar:** cerca de **1 hora passando gastos para planilha** virou sincronização **automática**.
- **AP Consultório:** chamar os pacientes no WhatsApp de **cerca de 30 minutos para 2 minutos**, com agenda e pagamentos sob controle.

**Como eu trabalho:** desenvolvo em co-participação com agentes de IA. O Claude Code implementa em uma branch, o Codex revisa o código e eu reviso cada alteração, rodo os testes e só então autorizo o commit. Levanto os requisitos com quem vai usar, defino critérios de aceite e documento a arquitetura de cada projeto.

## Projetos em uso

### Catálogo B2B — ProAventura
**Problema:** a equipe comercial mandava PDF para cada revendedor que queria cotar um produto, e cada cotação levava mais de 1 hora.
**Solução:** portal de cotação com login para revendedores e equipe, filtros, carrinho de cotação e painel interno.
**Resultado:** a cotação caiu de **mais de 1 hora para 10 a 15 minutos** (cerca de 80% menos tempo), comparando o mesmo atendimento antes e depois do portal.
**Arquitetura:** login pelo Supabase Auth (JWT); o PostgreSQL decide o acesso com Row Level Security, e o preço de revenda só sai do banco para revendedor aprovado. Integrações rodam no servidor (Edge Functions): estoque do ERP Bling via OAuth 2.0 e webhook com assinatura HMAC, e notificação de cotação por WhatsApp.
**Stack:** JavaScript, PostgreSQL (Supabase), Edge Functions, Netlify.
**Status:** em desenvolvimento, com uso piloto · código privado · [página pública do projeto](https://github.com/daniloptoledo/catalogo-proaventura)

![Catálogo B2B ProAventura — catálogo do revendedor com filtros, selos e cotação (produtos e preços fictícios)](assets/catalogo-capa.png)

### Sistema de Chamada da Crisma
**Problema:** a presença dos jovens em encontros e missas era controlada em planilha, e cada chamada levava de 10 a 15 minutos.
**Solução:** app para a equipe de catequistas registrar presença, com indicadores de faltas por tipo de evento, alerta conforme a regra da coordenação e importação do histórico em Excel (com prévia e sem duplicatas).
**Resultado:** a chamada caiu de **10 a 15 minutos para 2 minutos**, com 102 jovens em 5 grupos já no sistema.
**Arquitetura:** backend em JavaScript no Cloudflare com banco SQL (D1); PIN guardado com PBKDF2, sessão em cookie HttpOnly e permissões checadas no servidor a cada rota, com auditoria. Privacidade é requisito central (dados de menores).
**Qualidade:** testes de API, regras e banco rodando no GitHub Actions a cada pull request.
**Stack:** React, JavaScript, SQL (Cloudflare D1).
**Status:** em uso desde out/2026 · código privado

![Sistema de Chamada da Crisma — dashboard e chamada no celular (dados fictícios)](assets/crisma-capa.png)

### Financeiro Familiar
**Problema:** organizar as finanças da casa exigia cerca de 1 hora passando gastos e dados bancários para uma planilha.
**Solução:** sincronização bancária diária via Open Finance, conciliação entre contas PF e PJ, detecção de transferências internas e duplicidades e projeção de fluxo de caixa.
**Resultado:** o lançamento manual de cerca de **1 hora virou automático**.
**Arquitetura:** o navegador só calcula o que exibe; escritas críticas (baixa de pagamento, parcelas) são funções atômicas no PostgreSQL, protegidas por RLS; integrações bancárias e notificações rodam em rotas de servidor na Vercel. Nenhuma credencial bancária é armazenada.
**Qualidade:** testes automatizados e CI no GitHub Actions; backup diário cifrado.
**Stack:** TypeScript, Next.js, PostgreSQL (Supabase), Vercel.
**Status:** em uso pela família · código privado

![Financeiro Familiar — visão do mês no computador e no celular (dados fictícios)](assets/financeiro-capa.png)

### AP Consultório
**Problema:** a psicóloga se perdia na agenda e levava cerca de 30 minutos para chamar os pacientes da semana.
**Solução:** app instalável (PWA) de agenda, pacientes, evolução clínica e financeiro, com lembrete por notificação push e atalho para chamar o paciente no WhatsApp.
**Resultado:** chamar os pacientes caiu de **cerca de 30 minutos para 2 minutos**; a agenda ficou organizada e dá para ver quem já pagou.
**Arquitetura:** RLS por dono em todas as tabelas; prontuário só pode ser criado e lido, nunca editado ou apagado; envio de notificações por Edge Function protegida por segredo.
**Stack:** React, TypeScript, PostgreSQL (Supabase), Web Push.
**Status:** em uso · código privado (dados de saúde)

## Em construção

### Pipeline de Pedidos de Marketplace
**O que é:** pipeline ETL em **Python** que lê pedidos do Mercado Livre e da Amazon (com formatos diferentes), limpa e valida os dados com **Pandas** e grava num **PostgreSQL** rodando em **Docker**. Linhas inválidas vão para uma tabela de rejeitados, com o motivo.
**Destaques:** constraints e chaves no banco como segunda barreira de validação; carga idempotente (rodar duas vezes não duplica); testes com pytest. Dados 100% sintéticos.
**Próximas etapas:** KPIs com SQL, API REST com FastAPI e login JWT, CI no GitHub Actions.
**Status:** etapa 1 em andamento · [código](https://github.com/daniloptoledo/pipeline-pedidos-marketplace)

## Outros projetos

### Sinalizador de Câmeras de Estúdio
Sinalização luminosa que mostra ao apresentador qual câmera está no ar, lendo a mesa de corte Blackmagic ATEM Mini Pro. Projeto Integrador do 4º semestre, feito para o estúdio da Comunidade Católica Pantokrator; próxima etapa sem fio com ESP32 (iniciação científica 2027).
**Stack:** Python, C/C++ (Arduino), ESP32. **Status:** protótipo funcional · [vídeo de demonstração](https://youtu.be/DR60vTPyErs) · [site](https://sinalizador-cameras-site.pages.dev) · [código](https://github.com/daniloptoledo/sinalizador-cameras-estudio)

[![Sinalizador de Câmeras — vídeo de demonstração do Projeto Integrador](https://i.ytimg.com/vi/DR60vTPyErs/hqdefault.jpg)](https://youtu.be/DR60vTPyErs)

## Habilidades

- **IA aplicada:** desenvolvimento com agentes de IA (Claude Code, Codex), engenharia de prompts, revisão e teste do que a IA produz
- **Dados:** SQL (PostgreSQL, SQLite), modelagem relacional, importação e validação de dados
- **Integrações:** APIs REST, webhooks, OAuth 2.0, autenticação JWT
- **Linguagens:** JavaScript/TypeScript; Python em desenvolvimento no projeto de pedidos
- **Ferramentas:** Git/GitHub (branches, pull requests, GitHub Actions), Docker, Excel, ERP Bling
- **Processo:** SDLC (requisitos, testes, documentação, manutenção) e definição de KPIs

## Procurando

Estágio em **IA aplicada, automação, dados, produto ou QA**, para aprender e contribuir em problemas reais.
