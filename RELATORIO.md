# Relatório: catálogo, pacotes e regra de comissão v3 (08/11/2026)

O sistema foi atualizado a partir do código existente. Nada foi reconstruído e nenhuma função foi removida. Tudo entrou numa migração nova, `supabase/migrations/20261108000001_catalogo_comissoes_v3.sql`, que não apaga dados. Contratos aprovados nas regras v1 e v2 continuam calculando exatamente como antes.

O relatório anterior (21/10) descrevia CRM, projetos guiados, comissões v2 e Mercado Pago. Tudo isso continua no sistema.

## O que mudou

1. **Catálogo de serviços**
   - Os 17 serviços do documento, com faixas de preço de implantação e de mensalidade, todas editáveis em Configurações.
   - "Fotografias de produtos" é cobrada por foto (quantidade × preço).
   - O WhatsApp com IA traz descrito o que a mensalidade inclui.
   - A gestão básica de redes registra os 2 vídeos por semana.
2. **Pacotes**
   - Presença Digital, Vendas Inteligentes e Operação Integrada.
   - Cada pacote é uma lista de serviços com preço próprio.
   - No projeto dá para tirar ou adicionar serviços e mudar valores; o total é recalculado.
3. **Regra de comissão v3**
   - Projetos: reserva de 10%, 20% para quem trouxe e executa, valor fixo para quem só indicou, saldo dividido entre a equipe.
   - Mensalidades: 40% para quem trouxe e continua responsável ativo, reserva mínima de 10% e parte opcional para quem executa o serviço mensal.
   - Fica versionada como as anteriores e é fixada na aprovação.
4. **Responsável ativo**
   - Cada contrato tem um responsável ativo, com histórico.
   - A troca é feita só pela Gestão, com data e justificativa.
   - A troca não mexe em comissões já geradas.
5. **Indicadores externos**
   - Tela própria com contato, PIX, comissão padrão, clientes indicados, projetos fechados, a pagar e pago.
   - O pagamento é confirmado na ficha do indicador.
6. **Clientes e projetos**
   - Um cliente pode ter vários projetos e mensalidades.
   - Cada projeto guarda os serviços com preço individual, o pacote, quem fez a venda, o responsável ativo, a equipe, as parcelas e as comissões.
   - O sistema marca as vendas adicionais e guarda quem trouxe o cliente originalmente.
7. **Painel individual** (Início e Comissões)
   - Clientes que trouxe, projetos vendidos, serviços vendidos, clientes sob responsabilidade e mensalidades ativas.
   - Comissões de projetos, recorrentes e de indicação, cada uma com previsto, liberado e pago.
   - Ganhos acumulados e saldo pendente.
   - A Gestão vê o painel de qualquer pessoa.
8. **Financeiro**
   - Faturamento, comissões (equipe e indicadores), reserva empresarial, custos operacionais e resultado, no mês, no ano ou nos últimos 12 meses, também mês a mês.
   - Novo cadastro de despesas.
   - O Mercado Pago continua igual: pagamentos parciais, taxas e estornos.

## Base de cálculo e Mercado Pago (o ponto que o documento deixou em aberto)

A comissão é calculada sobre o **valor integral** pago pelo cliente.

A taxa do Mercado Pago continua registrada em cada recebimento. Ela entra no Financeiro como custo operacional, pago pela parte da Névora. Assim, a conta sempre fecha:

> faturamento = comissões + parte da Névora (reserva + demais) + custo de produção
>
> resultado = faturamento − comissões − custos operacionais

Um teste confere esse fechamento com uma taxa real de Mercado Pago e com estorno. Se a Névora preferir voltar à base líquida, basta criar uma nova versão da regra com a opção desmarcada.

## O que foi testado

| Teste | Resultado |
|---|---|
| Banco: 61 execuções em 6 grupos: v1, atualização v1→v2, v2, **v2 no banco novo**, **atualização v2→v3** e **v3** | Passando |
| Exemplos do documento: projeto de R$ 5.000 com captador executor (1.000 / 500 / 3.500) e com indicação (300 / 500 / 4.200); mensalidade de R$ 1.500 (600 / 900) | Iguais ao centavo |
| Simulação do formulário × lançamento real × prévia, num projeto com pacote, fotos, mensalidade e executores | Iguais ao centavo |
| Navegador (Playwright), fluxo do colaborador ao gestor: orçamento com pacote + 30 fotos, simulação, envio, aprovação, troca de responsável, financeiro, indicadores, configurações e painel por pessoa | Sem erros no console |
| Celular (iPhone 13): sem rolagem lateral em nenhuma tela | Ok |

Durante a verificação no navegador, corrigi três problemas:
- Ao editar um campo e clicar direto em "Continuar", o clique se perdia.
- A barra de passos do cadastro ficava achatada quando o conteúdo era longo.
- No celular, uma grade do Início causava rolagem lateral.

**Limites da verificação:** nesta máquina não havia PostgREST nem Deno. As telas foram testadas contra um substituto local do PostgREST, ligado ao mesmo banco e às mesmas permissões. Por isso, o teste `tests/e2e/painel.test.mjs`, já atualizado para o formulário novo, só rodou até a criação do link do Mercado Pago, que precisa das funções em Deno. A parte do Mercado Pago foi conferida pelos testes do banco, mas falta rodar o teste completo no ambiente do `dev/iniciar.sh` e testar com a conta real.

## Escolhas que fiz e você pode mudar

1. **Cliente trazido pela Gestão ou pelo canal da Névora:** os 20% de captação ficam com a Névora (30% no total, com a reserva) e a equipe recebe o mesmo saldo de quando um colaborador traz. Isso fica configurável em Configurações > Regra de comissão.
2. **Gestor que traz um cliente:** conta como cliente da Névora, como já era. Se ele executar, recebe a parte dele no saldo.
3. **Composição dos pacotes:** o documento trazia só os totais, então montei:

   | Pacote | Serviços |
   |---|---|
   | Presença Digital | Landing page R$ 1.200 + R$ 149/mês e Identidade visual R$ 700 |
   | Vendas Inteligentes | Site institucional R$ 2.000 + R$ 99/mês e WhatsApp com IA R$ 2.500 + R$ 500/mês |
   | Operação Integrada | Sistema de gestão R$ 5.000 + R$ 450/mês, Integração site + painel R$ 1.500 + R$ 150/mês e Automações internas R$ 1.500 + R$ 299/mês |

   Tudo é editável em Configurações > Pacotes.
4. **Indicação:** o valor fixo sai do saldo da execução, como no exemplo do documento. O sistema recusa um valor maior que o projeto sem a reserva. A faixa de R$ 100 a R$ 500 é só referência.
5. **Os 40% da mensalidade:** valem conforme quem é o responsável na data de vencimento de cada mensalidade. "Não automaticamente" virou uma exceção que a Gestão pode autorizar ao trocar o responsável.
6. **Venda adicional:** os 20% e os 40% vão para quem fez aquela venda, e o cliente continua registrado com quem o trouxe primeiro.
7. **Contato e PIX dos indicadores:** só a Gestão vê. A equipe vê apenas o nome, para escolher no cadastro do projeto.
8. **Serviços antigos:** Site, Sistema, Automação e Social media ficaram desativados e guardados para os contratos antigos.

## Atualização de 09/11/2026: placas NFC retiradas

- Migração `20261109000001_retirar_nfc.sql`: o serviço "Placas NFC" e as tarefas padrão dele ficaram desativados, e uma regra no banco impede que voltem a ficar ativos.
- O cadastro de projeto não tem mais o caminho de placas. O serviço também não aparece mais em Configurações > Serviços e preços, nem na lista de desativados.
- Nada foi apagado. Se existir algum contrato antigo de placas, ele continua com os valores, as cobranças e as comissões que já tinha.
- Testes: a v3 confere que NFC não entra em orçamento, não é vendida sozinha e não pode ser reativada. A regressão v2 continua conferindo o cálculo antigo das placas, reativando o serviço só dentro do teste.

## O que ainda falta para colocar no ar

São os mesmos itens do relatório anterior: projeto Supabase, repositório, credenciais do Mercado Pago, Cloudflare Pages e os nomes reais da equipe. Num banco que já está no ar, o `supabase db push` aplica só a migração nova. O passo a passo está no README, na seção "Colocar no ar".
