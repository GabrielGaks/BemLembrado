# Bem Lembrado

Painel web do MVP de um assistente de lembretes para pessoas idosas, integrado ao WhatsApp. O responsável cadastra pessoas, contatos e lembretes; o backend registra envios e confirmações e alerta um contato autorizado quando necessário.

## Stack atual

- Next.js 16, React 19 e TypeScript: painel e APIs
- Supabase Auth + PostgreSQL/RLS: autenticação e dados
- Evolution API: conexão com o WhatsApp
- Worker Node.js: relay da fila de mensagens
- Regras determinísticas: interpretação de lembretes e fluxos críticos

## Começar localmente

1. Execute `npm ci`.
2. Copie `.env.example` para `.env.local` e preencha as variáveis do Supabase.
3. Aplique as migrations de `supabase/migrations` no projeto Supabase.
4. Execute `npm run dev` e abra `http://localhost:3000`.

Sem variáveis do Supabase, a página inicial continua disponível com dados demonstrativos.

## Limites do MVP

O sistema apoia a rotina, mas não diagnostica, prescreve, altera doses nem funciona como serviço de emergência. Horários, medicamentos e regras críticas são dados cadastrados e controlados por regras; não ficam sob decisão da IA.

## MVP com WhatsApp

O MVP usa uma conexão **não oficial** via Evolution API/WhatsApp Web. Ela não cobra por mensagem da Meta, mas exige infraestrutura própria continuamente ligada e o número pode ser desconectado ou bloqueado. Não use um número pessoal principal nem faça disparos em massa.

O fluxo implementado é: Evolution → webhook idempotente → Supabase → lembretes/outbox → relay local → Evolution. Consulte [docs/MVP_WHATSAPP.md](docs/MVP_WHATSAPP.md) para configurar e testar.

## Validação

```bash
npm test
npm run lint
npm run build
```
