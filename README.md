# RotaCerta — kit inicial de assinaturas e vendas

Este kit NÃO instala cobrança no app sozinho, NÃO gera links reais e NÃO altera automaticamente o seu repositório. Ele fornece preços, um esquema SQL opcional e textos comerciais para começar.

## 1. Comece a vender com links de assinatura

1. No Mercado Pago, abra Ferramentas para vender > Assinaturas > Criar plano (os nomes das opções podem mudar).
2. Crie três planos mensais: RotaCerta Básico (R$149), Profissional (R$299) e Empresarial (R$499).
3. Copie os links de assinatura e envie-os às transportadoras por WhatsApp ou e-mail.
4. Antes de liberar o acesso de uma empresa, confirme o pagamento dentro do painel oficial do Mercado Pago. Não confie apenas em print/comprovante encaminhado.
5. Registre empresa, responsável, plano, vencimento, motoristas autorizados e confirmação da cobrança.

## 2. Como aproveitar os arquivos

- `src/config/rotacertaPlans.ts`: preços e limites para integrar à interface React do seu sistema. Você precisa conectá-los às telas reais.
- `supabase/001_rotacerta_assinaturas.sql`: MODELO OPCIONAL de tabela de assinaturas. Não execute sem comparar com sua estrutura real de empresas, usuários e permissões. Requer integração de backend.
- `vendas/mensagem-whatsapp.txt`: mensagem inicial para prospectar clientes.
- `vendas/proposta-comercial.md`: proposta de venda editável.

## 3. Próxima etapa técnica: automação com segurança

1. Identifique a transportadora na base de dados (`company_id`).
2. Crie vínculo entre cada empresa e sua assinatura no provedor.
3. Configure um endpoint/backend protegido para receber notificações do provedor.
4. Valide a autenticidade da notificação e consulte o pagamento na API oficial quando necessário.
5. Somente backend confiável atualiza status `active`, `past_due` ou `canceled`.
6. O backend precisa impor limites de motoristas e verificar a assinatura em cada recurso pago: não basta esconder botões na tela.
7. Configure política de leitura por membro da transportadora (RLS) com base nas tabelas reais.
8. Teste pagamentos, falhas, vencimentos e cancelamentos em ambiente de teste antes de usar dinheiro real.

**Nunca** coloque segredo de API, senha, chave `service_role` ou token privado em código do app ou repositório.

## 4. Vendas e cuidados

- Faça uma demonstração real do que já funciona; não prometa rastreamento ao vivo ou emissão de relatórios se ainda não foram implementados.
- Tenha termos claros de cobrança, suporte, cancelamento, dados e privacidade.
- A LGPD pode se aplicar ao tratamento de dados de motoristas, inclusive localização.
- Se você distribuir o Android pelo Google Play, verifique as políticas de pagamento antes de colocar links de compras externas dentro do aplicativo. A venda por contato comercial externo é um fluxo distinto.
- Verifique requisitos da conta de pagamentos e da formalização do negócio, com apoio de responsável legal se necessário.

## 5. Uso no Android/GitHub Codespaces

Abra o repositório em Codespaces, crie as pastas indicadas e copie os arquivos correspondentes. NÃO envie o ZIP esperando que o GitHub extraia automaticamente os arquivos. Teste a mudança em uma branch e faça backup do projeto antes de executar SQL ou mexer na autenticação.

Documentação:
- Mercado Pago (planos): https://www.mercadopago.com.br/developers/pt/docs/subscription-plans/create-subscription-plan
- Supabase (RLS): https://supabase.com/docs/guides/database/postgres/row-level-security
- Google Play (pagamentos): https://support.google.com/googleplay/android-developer/answer/9858738?hl=pt-BR
