# Painel Névora

Sistema interno da Névora: CRM de oportunidades, carteira de clientes, catálogo com pacotes, projetos com vários serviços e tarefas, comissões (regra v3), indicadores externos e financeiro com Mercado Pago.
Stack: Supabase (Postgres, login, tempo real, Edge Functions) e Cloudflare Pages (hospeda a pasta `web/`).

## Estrutura

| Pasta | Conteúdo |
|---|---|
| `supabase/migrations/` | Banco completo com permissões (RLS) no próprio banco. As de 21/10/2026 trazem CRM, comissões v2 e Mercado Pago. A de 08/11/2026 traz catálogo, pacotes, regra v3, responsável ativo, indicadores e financeiro. A de 09/11/2026 retira as placas NFC. Nenhuma apaga dados |
| `supabase/functions/` | `mp-webhook` (recebe avisos do Mercado Pago), `mp-criar-link`, `mp-verificar`, `convidar-usuario` |
| `web/` | O painel (HTML + JavaScript, sem build). `web/config.js` recebe a URL e a chave pública do Supabase |
| `tests/` | Testes do banco (`run.sh`), do Mercado Pago (`e2e/mercadopago.test.mjs`) e do painel no navegador (`e2e/painel.test.mjs`) |
| `dev/` | Ambiente local parecido com o Supabase, para testar tudo sem conta, e `dados-exemplo.sql` |
| `prototipo/` | Protótipo antigo, só referência visual |

## Telas

- **Início:** os resultados da pessoa e o que fazer hoje. Mostra saldo pendente, ganhos acumulados, previsto, mensalidades ativas (40%), clientes que trouxe, projetos vendidos, clientes sob responsabilidade e serviços vendidos. Também mostra as próximas reuniões, as tarefas, os projetos, as oportunidades e os clientes. A Gestão vê também os projetos aguardando aprovação.
- **Oportunidades:** funil em colunas com arrastar e soltar, reunião com data e hora, linha do tempo, aviso de duplicidade e conversão em cliente.
- **Clientes:** "Meus clientes" e "Todos os clientes". Um cliente pode ter vários projetos e mensalidades. Cada projeto mostra o responsável e se foi uma venda adicional.
- **Projetos:** cadastro em 7 passos:
  1. **Cliente.**
  2. **Serviços:** pacote ou serviços avulsos, com preço editável, fotos por quantidade e aviso de valor fora da faixa.
  3. **Origem:** colaborador, Gestão, canal da Névora ou indicador externo.
  4. **Equipe:** quem executa, captador ou indicação, responsável ativo e parte da mensalidade para os executores.
  5. **Valores.**
  6. **Resumo:** a simulação pela regra vigente.
  7. **Enviar.**

  A Gestão aprova ou devolve. A página do projeto mostra os serviços com preço, as comissões por pessoa, o histórico de responsáveis e o botão **Trocar responsável** (Gestão).
- **Minhas tarefas:** sem mudança. As tarefas padrão agora são criadas para todos os serviços do projeto.
- **Comissões:** o painel individual com projetos, recorrentes e indicações (previsto, liberado e pago). A Gestão tem "A pagar" (equipe e indicadores), "Resultados por pessoa" e "Pagamentos feitos".
- **Financeiro:**
  - Gestão: **resultado da Névora** no mês, no ano ou nos últimos 12 meses, com faturamento, comissões, reserva empresarial, custos operacionais e resultado, mês a mês. Tem ainda as cobranças (Mercado Pago, recebimento manual, estorno) e **Custos e despesas** (hospedagem, APIs, ferramentas, taxas, produção e outras).
  - Colaborador: as cobranças dos projetos em que participa.
- **Indicadores (Gestão):** quem traz clientes sem executar. Mostra contato, PIX, comissão padrão, clientes indicados, projetos fechados, comissão acordada, a pagar e pago, com confirmação de pagamento.
- **Configurações (Gestão):** equipe, etapas do funil e origens. Também traz:
  - **Serviços e preços:** grupo, cobrança, faixas de implantação e mensalidade, preço por unidade, o que inclui e regra de comissão.
  - **Pacotes:** serviços, quantidades e preços de cada pacote.
  - **Regra de comissão:** a regra vigente, novas versões e o histórico.

## Catálogo

Os preços são referências iniciais e podem ser editados em Configurações. Em cada projeto, o valor pode ser ajustado.

| Grupo | Serviços |
|---|---|
| Tecnologia | Landing page, Site institucional, Loja virtual, Painel administrativo básico, Sistema de gestão personalizado, Sistema de logística e estoque, Integração site + painel, Fotografias de produtos (R$ 2 a R$ 20 por foto) |
| IA e automações | WhatsApp com IA (a partir de R$ 250/mês, com atendimento, qualificação, acompanhamento, follow-up e recuperação incluídos), Automações internas, Integração com sistemas externos |
| Marketing | Gestão básica de redes (pelo menos 2 vídeos por semana), Gestão completa de redes, Vídeo institucional (orçamento), Identidade visual, Gestão de tráfego pago, Consultoria de crescimento |

Pacotes: **Presença Digital** (R$ 1.900 + R$ 149/mês), **Vendas Inteligentes** (R$ 4.500 + R$ 599/mês) e **Operação Integrada** (a partir de R$ 8.000 + R$ 899/mês). Cada pacote é uma lista de serviços com preço próprio.

**Placas NFC foram retiradas** (migração `20261109000001_retirar_nfc.sql`): o serviço não aparece mais no catálogo e o banco impede que ele seja reativado. Os serviços genéricos antigos (Site, Sistema, Automação e Social media) também ficaram desativados. Nada foi apagado: os contratos antigos desses serviços continuam guardados e calculando como antes.

## Regras de comissão (v3)

Contas em centavos, e a soma nunca passa do valor pago. A regra vigente fica gravada no projeto **no momento da aprovação**. Contratos aprovados nas regras v1 e v2 não mudam.

**Projetos** (exemplo: R$ 5.000):

| Situação | Divisão | Exemplo |
|---|---|---|
| Quem trouxe o cliente e executa | 10% reserva da Névora, 20% captação, saldo dividido igualmente pela equipe (o captador incluído) | R$ 500 + R$ 1.000 + R$ 3.500 |
| Quem só indicou (colaborador fora da equipe ou indicador externo) | 10% reserva, valor fixo combinado, saldo para a equipe | R$ 500 + R$ 300 + R$ 4.200 |
| Cliente da Gestão ou do canal da Névora | 10% reserva + 20% captação ficam com a Névora, saldo para a equipe | R$ 1.500 + R$ 3.500 |

**Mensalidades** (sites, sistemas, IA e redes sociais; exemplo: R$ 1.500):

| Situação | Divisão |
|---|---|
| Trouxe o cliente **e** é o responsável ativo | 40% para essa pessoa (R$ 600), 60% Névora e operação (R$ 900, com reserva mínima de 10%) |
| Trouxe, mas deixou de ser responsável | Os 40% ficam com a Névora nas mensalidades seguintes |
| É responsável, mas não trouxe | Não recebe, a não ser que a Gestão autorize a exceção ao trocar o responsável |
| Só indicou | Não recebe mensalidade |

Outras regras:
- Dentro dos 60%, o projeto pode destinar uma parte aos **executores da mensalidade** (por exemplo, quem faz a gestão de redes). O sistema não deixa a reserva ficar abaixo de 10%.
- **Troca de responsável:** só a Gestão faz, com data e justificativa. Comissões já geradas não mudam. Vale para as mensalidades que vencem a partir da data escolhida.
- **Venda adicional:** o cliente guarda quem o trouxe primeiro, e cada projeto guarda quem fez aquela venda. Os 20% e os 40% vão para quem fez a venda.
- **Base de cálculo:** comissões sobre o **valor integral** pago pelo cliente. As taxas do Mercado Pago e os impostos ficam como custo operacional da Névora e aparecem no Financeiro. A regra tem uma opção para voltar à base líquida.
- A comissão é liberada na proporção do que o cliente pagou, incluindo a indicação fixa.
- Em projetos com serviços configurados como "100% Névora", só a parte dos serviços de execução entra na divisão.

Situações de cobrança e comissão: Previsto, Aguardando, Parcial, Atrasado, Recebido, Comissão liberada, Comissão paga e Cancelado/estornado. Só a Gestão confirma que uma comissão foi paga.

## Mercado Pago

Todo pagamento cai na conta da Névora, sem split.

1. Na cobrança, a Gestão clica em **Gerar link de pagamento**. A função `mp-criar-link` cria uma preferência com `external_reference = cobranca:<id>`.
2. O Mercado Pago avisa `mp-webhook`. A função confere a assinatura `x-signature` (HMAC com a chave secreta) e **busca o pagamento na API do Mercado Pago**, sem confiar no corpo do aviso. Só depois registra.
3. O registro é idempotente: a referência `mp:<payment_id>` é única, então avisos repetidos não duplicam nada. A taxa do Mercado Pago fica registrada no recebimento. Na regra v3 ela vira custo da Névora (a comissão é sobre o valor integral); nos contratos v2 continua descontada da base.
4. Um estorno ou chargeback total cancela as comissões ou cria um ajuste negativo, se elas já tinham sido pagas. Um estorno parcial é registrado como erro para ajuste manual.
5. **Verificar pagamento** (`mp-verificar`) busca no Mercado Pago os pagamentos da cobrança, caso algum aviso tenha se perdido.
6. Tudo fica em `mp_eventos`. Os tokens existem só nas variáveis secretas das funções; o navegador nunca os vê.

## Testes

```bash
# Banco (Postgres 15+): 61 execuções em 6 grupos
#   v1, atualização v1→v2, v2, v2 no banco atual, atualização v2→v3 e v3
PGHOST=... PGPORT=... PGUSER=postgres bash tests/run.sh

# Ambiente local completo (Postgres + PostgREST + funções em Deno + gateway em http://localhost:54321)
PGHOST=... PGPORT=... PGUSER=postgres POSTGREST=/caminho/postgrest RECRIAR=1 bash dev/iniciar.sh
psql -d nevora_dev -f dev/dados-exemplo.sql      # opcional: clientes, contratos e pagamentos de exemplo
PORTA=54500 node dev/mock-mercadopago.mjs &      # Mercado Pago simulado
ANON_KEY=... node tests/e2e/mercadopago.test.mjs  # chave em /var/tmp/nevora-dev/chaves.env
PLAYWRIGHT=$(npm root -g)/playwright/index.mjs node tests/e2e/painel.test.mjs
```

Logins locais: `gestor@nevora.local`, `colaborador1@nevora.local`, `colaborador2@nevora.local` e `colaborador3@nevora.local`, todos com a senha `nevora123`.

Os testes da v3 (`tests/v3/`) cobrem:
- os exemplos do documento (R$ 5.000 e R$ 1.500);
- indicação de colaborador e de indicador externo, inclusive com pagamento parcial;
- troca de responsável e a exceção autorizada;
- executores da mensalidade e a reserva mínima;
- base integral com taxa do Mercado Pago, estorno e fechamento do financeiro;
- pacotes, fotos, serviços "100% Névora" e venda adicional;
- simulação igual ao lançamento real, centavo a centavo;
- painel individual, privacidade e travas depois da aprovação.

O teste do navegador percorre o fluxo inteiro: um colaborador cria a oportunidade, converte em cliente e cadastra o projeto; a Gestão aprova; outra pessoa trabalha nas tarefas; o pagamento parcial chega pelo webhook; a comissão é liberada na proporção e a Gestão confirma o pagamento.

## Colocar no ar

1. **Supabase:** crie o projeto e rode `supabase link --project-ref <ref>` e depois `supabase db push`. Num projeto que já está no ar, o `db push` aplica só as migrações novas (`20261108000001_catalogo_comissoes_v3.sql` e `20261109000001_retirar_nfc.sql`), sem apagar dados.
2. **Primeiro acesso da Gestão:** em Authentication, crie o usuário do gestor e rode no SQL Editor:
   ```sql
   insert into public.perfis (id, nome, papel, email)
   select id, 'Nome do gestor', 'gestao', email from auth.users where email = 'gestor@exemplo.com';
   ```
   O restante da equipe é convidado pelo painel, em Configurações e depois Equipe.
3. **Funções:**
   ```bash
   supabase secrets set MP_ACCESS_TOKEN=APP_USR-... MP_WEBHOOK_SECRET=... SITE_URL=https://painel.nevora.com.br
   supabase functions deploy mp-webhook --no-verify-jwt
   supabase functions deploy mp-criar-link mp-verificar convidar-usuario
   ```
4. **Mercado Pago:** em Suas integrações e depois Webhooks, cadastre `https://<ref>.supabase.co/functions/v1/mp-webhook` com o evento *Pagamentos* e copie a chave secreta para `MP_WEBHOOK_SECRET`.
5. **Cloudflare Pages:** publique a pasta `web/` (sem build) e preencha `web/config.js` com a URL do projeto e a chave **anon** (pública).
6. **Supabase Auth:** coloque o endereço do painel em *Site URL* e *Redirect URLs*, para os convites e a troca de senha.
7. **Opcional:** agende `gerar_mensalidades(current_date)` todo mês no `pg_cron`.

As migrações deixam o banco no horário de Brasília (`timezone = America/Sao_Paulo`), para que vencimentos e atrasos batam com o calendário da equipe.
