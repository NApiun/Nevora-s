# Névora: visão geral do aplicativo

O painel interno da Névora organiza o trabalho comercial e de entrega de ponta a ponta. Ele começa no primeiro contato com uma empresa e termina no pagamento da comissão de cada pessoa da equipe.

**Por que existe:** antes, a prospecção, os projetos, as tarefas e as comissões ficavam espalhados, e a conta de quem recebe quanto era manual. Agora tudo fica num lugar só, com regras automáticas, histórico de cada mudança e permissões que protegem os valores.

---

## 1. O caminho principal

```
Captação → Orçamento (pacote ou serviços) → Projeto → Aprovação da Gestão → Execução → Mensalidades → Pagamentos → Comissões → Resultado financeiro
```

Cada etapa alimenta a próxima. Ninguém precisa redigitar dados nem refazer contas.

---

## 2. Quem usa e o que cada um pode fazer

| Perfil | O que faz | Por quê |
|---|---|---|
| **Gestão** | Vê tudo, aprova ou devolve projetos, confirma pagamentos de comissão, configura etapas, origens, serviços, regras e equipe | Alguém precisa validar valores antes de virarem dinheiro de verdade |
| **Colaborador** | Cria e atualiza oportunidades, cadastra clientes e projetos, cuida das tarefas e acompanha os próprios resultados e comissões | Cada pessoa lança o próprio trabalho, sem depender da Gestão para digitar |
| **Indicador externo** (sem login) | Traz clientes, mas não participa da execução. Recebe uma comissão fixa por indicação convertida | A Gestão acompanha e paga cada indicação pelo painel |

**Regra de privacidade:**
- Todos veem a carteira de clientes, com nome, segmento e serviços.
- Valores, cobranças e comissões de um projeto só aparecem para quem participa dele e para a Gestão.
- Essa regra vale no **banco de dados**, não só na tela. Mesmo alguém que tente acessar por fora não recebe esses dados.

---

## 3. Ferramentas, uma a uma

### 3.1 Início
**O que mostra:**
- **Meus resultados:**
  - saldo pendente (liberado e ainda não transferido);
  - ganhos acumulados;
  - previsto;
  - mensalidades ativas com direito aos 40%;
  - clientes que trouxe, projetos vendidos (com as vendas adicionais), clientes sob minha responsabilidade e serviços vendidos.
- As próximas reuniões.
- As minhas tarefas, separadas em atrasadas, em andamento e pendentes.
- Meus projetos, minhas oportunidades e meus clientes.
- Para a Gestão, os projetos aguardando aprovação.

**Atalhos:** "+ Nova oportunidade" e "+ Novo projeto".

**Por quê:** cada pessoa abre o painel e já sabe o que fazer hoje e quanto tem a receber.

### 3.2 Oportunidades (CRM)
**Como funciona:**
- É um funil em colunas, como um quadro Kanban, em que você arrasta a empresa de uma etapa para outra.
- **Campos:**
  - Obrigatórios: empresa e Instagram.
  - Opcionais: site, contato, WhatsApp, serviço de interesse, origem, captador, responsável, próxima reunião, valor da proposta e observações.
- **Captador e responsável:**
  - O captador já vem preenchido com quem cadastrou, mas pode ser outra pessoa.
  - Depois de salvo, só a Gestão corrige o captador.
  - O responsável pode ser diferente do captador.
- **Reunião:** tem data e hora e aparece no Início. Remarcar fica registrado, por exemplo "Remarcou de 22/10 15h para 24/10 10h".
- **Linha do tempo:** guarda cada mudança (etapa, responsável, reunião, proposta, edições) e as anotações da equipe. Ninguém consegue apagar esse histórico.
- **Aviso de duplicidade:** ao digitar o nome ou o Instagram, o sistema avisa se a empresa já existe.

**Por quê:** ninguém perde um contato, todo mundo sabe em que pé está cada negociação, e fica registrado quem trouxe o cliente. Esse registro define a comissão de captação.

### 3.3 Conversão em cliente
**Como funciona:**
- Na oportunidade, clique em "Converter em cliente".
- O sistema procura cadastros parecidos por **nome, Instagram, domínio do site e WhatsApp**.
- Se achar algum, pergunta se é o mesmo cliente ou um cliente novo.
- Captador e histórico continuam ligados ao cliente.
- Em seguida, você já pode cadastrar o projeto.

**Por quê:** evita clientes duplicados e preserva quem captou.

### 3.4 Clientes
**Como funciona:**
- Duas abas: **Meus clientes**, que são os que eu captei ou em que participo de algum projeto, e **Todos os clientes**.
- Ao abrir um cliente:
  - Quem participa vê contato, WhatsApp, observações e projetos.
  - Quem não participa vê só as informações gerais.
- O botão "+ Novo cliente" também faz a verificação de duplicidade.

**Por quê:** a equipe conhece a carteira inteira sem expor valores de quem não está no projeto.

### 3.5 Projetos
**Cadastro guiado em 7 passos:**
1. **Cliente:** um cliente existente ou uma oportunidade convertida.
2. **Serviços:** um pacote (Presença Digital, Vendas Inteligentes, Operação Integrada) ou serviços avulsos do catálogo.
   - Cada serviço tem preço de implantação e de mensalidade, editáveis.
   - O sistema avisa quando o valor sai da faixa de referência.
   - Fotografias são cobradas por quantidade × preço por foto.
3. **Origem:** quem trouxe o cliente ou fez esta venda: um colaborador, a Gestão, o canal da Névora ou um indicador externo.
4. **Equipe:**
   - Quem executa o projeto. Se quem trouxe o cliente não estiver marcado, vira indicação, com valor fixo.
   - O **responsável ativo** pelo contrato.
   - A parte opcional da mensalidade para quem executa o serviço mensal.
5. **Valores:** total calculado pelos serviços, parcelas, forma de pagamento, início, prazo e dia da mensalidade.
6. **Resumo:** simulação de quanto cada pessoa recebe, com a regra aplicada.
7. **Enviar:** salvar como rascunho ou enviar para aprovação.

**Situações do projeto:** Rascunho, Aguardando aprovação, Em andamento, Entregue e Cancelado.

**Na aprovação, o sistema:**
- fixa a regra de comissão daquele dia;
- cria as cobranças (parcelas e mensalidades);
- cria as tarefas padrão de todos os serviços do projeto;
- registra o primeiro responsável ativo.

**Outras ações:**
- A Gestão pode **devolver para ajuste**, com um motivo.
- A **entrega ao cliente** exige confirmação explícita, mesmo com 100% das tarefas feitas.

**Página do projeto:**
- progresso, prazo, participantes, responsável ativo e serviços contratados com preço;
- o painel de comissões, com previsto, liberado e pago por pessoa;
- o histórico de responsáveis;
- o botão **Trocar responsável** (só a Gestão, com data, justificativa e, se combinado, a exceção dos 40%).

**Por quê:** cada colaborador lança o próprio projeto, vê quanto vai ganhar antes de enviar, e nada vira dinheiro sem a Gestão validar.

### 3.6 Tarefas (Minhas tarefas)
**Como funciona:**
- **Campos:** título, descrição, responsável, prazo, status (Pendente, Em andamento ou Concluída), autor e comentários.
- **Responsável:** precisa ser um participante do projeto. Também existem tarefas avulsas, sem projeto.
- **Concluir:** marque a caixinha.
- **Confirmações:** o sistema pede confirmação quando você **muda um prazo** ou **mexe na tarefa de outra pessoa**.
- **Histórico:** cada tarefa guarda quem mudou o quê e quando.
- **Abas:** "Comigo", "Que eu pedi" e "Dos meus projetos".

**Por quê:** a equipe se organiza sem um fluxo burocrático, e o histórico mostra quem fez o quê.

### 3.7 Comissões
**Para cada pessoa:**
- O painel individual, separado em **comissões de projetos**, **recorrentes** (40% das mensalidades) e **indicações simples**.
- Cada grupo mostra previsto, liberado e pago.
- Listas das minhas comissões liberadas, previstas e pagas.

**Para a Gestão:**
- O saldo a pagar de cada pessoa e de cada indicador externo, com a lista das comissões.
- **Resultados por pessoa:** o painel individual de qualquer colaborador.
- O botão "Confirmar pagamento", com data, forma e referência.
- O histórico de pagamentos feitos.

**Por quê:** transparência total sobre quanto cada um tem a receber. Só o gestor marca como pago.

### 3.8 Financeiro
**Como funciona:**
- **Resultado da Névora** (Gestão), no mês, no ano ou nos últimos 12 meses:
  - **Faturamento:** tudo que os clientes pagaram.
  - **Comissões:** equipe e indicadores.
  - **Reserva empresarial:** os 10% dos projetos e as demais receitas da Névora.
  - **Custos operacionais:** taxas do Mercado Pago, impostos, produção e despesas.
  - **Resultado:** faturamento − comissões − custos, também mês a mês.
- **Custos e despesas:** cadastro de hospedagem, APIs, ferramentas, taxas, produção e outras.
- **Cobranças:** a receber, em atraso, vence este mês e recebido do mês.
- **Cobranças:** cada uma tem uma situação: Aguardando, Parcial, Atrasado, Recebido ou Cancelado/estornado.
- **Ações da Gestão em cada cobrança:**
  - **Gerar link de pagamento** do Mercado Pago para enviar ao cliente.
  - **Verificar pagamento no Mercado Pago**, caso algum aviso tenha se perdido.
  - **Registrar recebimento manual**, para dinheiro ou transferência direta.
  - **Estornar** um recebimento.
- **Registro do Mercado Pago:** lista cada aviso recebido e o resultado.

**Por quê:** a Névora controla o que entrou, o que está atrasado e o que libera comissão.

### 3.9 Configurações (só a Gestão)
- **Equipe:** convidar pessoas por e-mail, trocar o papel, renomear e desativar sem apagar o histórico.
- **Etapas do funil:** criar, renomear, mudar a cor, o tipo e a ordem, e desativar. Desativar não apaga nenhuma oportunidade nem o histórico.
- **Origens:** por exemplo "Indicação" e "Perfil da Névora". Você marca quais contam como canal da Névora.
- **Serviços e preços:** catálogo por grupo (tecnologia, IA e automações, marketing). Cada serviço tem faixas de implantação e de mensalidade, preço sugerido, preço por unidade, o que inclui e a regra de comissão.
- **Pacotes:** os serviços, quantidades e preços de cada pacote.
- **Regra de comissão:** mostra a regra vigente, permite criar uma nova versão com motivo e mantém o histórico de versões.

**Por quê:** a operação muda com o tempo, e a Gestão ajusta sem mexer no código.

### 3.10 Indicadores (só a Gestão)
- Cadastro de quem traz clientes sem participar da execução: nome, WhatsApp, e-mail, PIX, observações e comissão padrão.
- Para cada indicador: clientes indicados, projetos fechados, comissão acordada, a pagar e já pago.
- Confirmação do pagamento direto na ficha do indicador.
- No cadastro do projeto, basta escolher "Indicador externo" e confirmar o valor combinado (referência de R$ 100 a R$ 500).

**Por quê:** as indicações viram um canal de vendas organizado, sem esquecer nenhum pagamento.

---

## 4. Regras de comissão (v3, desde 08/11/2026)

### Projetos (exemplo de R$ 5.000)
| Situação | Divisão | Exemplo |
|---|---|---|
| Trouxe o cliente e executa | 10% reserva da Névora + 20% captação + saldo para a equipe | R$ 500 + R$ 1.000 + R$ 3.500 |
| Só indicou (colaborador ou indicador externo) | 10% reserva + valor fixo (R$ 100 a R$ 500) + saldo para a equipe | R$ 500 + R$ 300 + R$ 4.200 |
| Cliente da Gestão ou do canal da Névora | 30% Névora (reserva + captação) + saldo para a equipe | R$ 1.500 + R$ 3.500 |

O saldo é dividido igualmente entre as pessoas marcadas na execução. Quem trouxe o cliente e executa recebe os 20% **e** a sua parte do saldo.

### Mensalidades (exemplo de R$ 1.500)
| Situação | Divisão |
|---|---|
| Trouxe o cliente e continua responsável ativo | 40% (R$ 600) para a pessoa, 60% (R$ 900) Névora e operação |
| Trouxe, mas deixou de ser responsável | Os 40% ficam com a Névora nas mensalidades seguintes |
| É responsável, mas não trouxe | Não recebe, a não ser por exceção autorizada pela Gestão |
| Só indicou | Não recebe mensalidade |

Dentro dos 60%, a reserva mínima de 10% é preservada, e o projeto pode destinar uma parte a quem executa o serviço mensal.

### Detalhes importantes
- **Responsável ativo:** cada contrato tem um. Só a Gestão troca, com data e justificativa. Comissões já geradas não mudam.
- **Venda adicional:** o cliente guarda quem o trouxe primeiro, e cada projeto guarda quem fez aquela venda.
- **Valor integral:** comissões sobre o que o cliente pagou. Taxas do Mercado Pago e impostos são custo da Névora.
- **Liberação proporcional:** se o cliente pagou 25% do projeto, 25% de cada comissão é liberada.
- **Contas em centavos:** a soma nunca passa do valor, e os centavos que sobram são distribuídos de forma justa.
- **A regra fica fixada na aprovação.** Contratos aprovados nas regras v1 e v2 continuam com a regra antiga.
- **Regra por serviço:** execução (as tabelas acima) ou "100% Névora".
- **Placas NFC:** retiradas em 09/11/2026. Não podem mais ser vendidas; contratos antigos, se houver, ficam guardados.

---

## 5. Mercado Pago

1. Todo pagamento cai na **conta da Névora**, sem divisão automática.
2. A Gestão gera o link e envia ao cliente.
3. Quando o cliente paga, o Mercado Pago avisa o sistema.
4. O sistema confere a **assinatura** do aviso e **consulta o pagamento direto na API do Mercado Pago**, para não confiar em avisos falsos.
5. O pagamento é registrado **uma vez só**, mesmo que o aviso chegue repetido. A taxa do Mercado Pago fica registrada e entra nos custos operacionais da Névora.
6. Um pagamento parcial libera comissão proporcional.
7. Um estorno total cancela as comissões ou gera um ajuste negativo, se elas já tinham sido pagas.
8. As chaves do Mercado Pago ficam só no servidor e nunca aparecem no navegador.

**Por quê:** a comissão só é liberada com dinheiro confirmado de verdade.

---

## 6. Segurança e histórico

- **Permissões no banco:** cada consulta respeita quem é a pessoa e se ela participa do projeto.
- **Histórico imutável:** oportunidades, tarefas, regras e pagamentos guardam cada mudança, e o histórico não pode ser apagado.
- **Nada é apagado à toa:** desativar etapas, origens, serviços ou pessoas preserva todo o histórico.
- **Tempo real:** quando alguém muda algo, a tela dos outros atualiza sozinha.
- **Horário de Brasília:** vencimentos e atrasos seguem o calendário da equipe.

---

## 7. Tecnologia

| Parte | Ferramenta | Função |
|---|---|---|
| Banco, login, tempo real | **Supabase** (Postgres) | Guarda os dados, aplica as regras e as permissões |
| Funções de servidor | **Supabase Edge Functions** | Mercado Pago (link, aviso, verificação) e convite de usuários |
| Site do painel | **Cloudflare Pages** | Hospeda as telas, a pasta `web/` |
| Pagamentos | **Mercado Pago** | Recebe o dinheiro dos clientes |

---

## 8. Testes

- **Banco:** 61 execuções de testes cobrem as regras v1, v2 e v3, as permissões, o CRM, a conversão, as tarefas, o Mercado Pago, o financeiro e as duas atualizações sem perder dados antigos.
- **Mercado Pago:** um teste contra uma API simulada confere o link, a assinatura, o registro, a duplicidade, a verificação e o estorno.
- **Navegador:**
  - O teste roda o fluxo completo com os 4 usuários: oportunidade, conversão, projeto, aprovação, tarefas, pagamento parcial e comissão paga.
  - Ele confirma que quem não participa não vê valores.
  - Ele confere a tela no celular.

---

## 9. O que falta para colocar no ar

1. Criar o projeto Supabase da Névora.
2. Criar o repositório no GitHub.
3. Cadastrar as credenciais do Mercado Pago: Access Token e chave do webhook.
4. Publicar o painel no Cloudflare Pages.
5. Trocar os nomes "Colaborador 1, 2, 3" pelos nomes reais.

O passo a passo técnico está no [README.md](README.md#colocar-no-ar).
