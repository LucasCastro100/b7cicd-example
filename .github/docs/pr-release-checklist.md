## Descrição

Traz todas as alterações da `develop` para a `main`:

- Guias movidos para `.github/docs/`
- `README.md` atualizado (stack, pré-requisitos, estrutura e contribuição)
- Migração do `package-lock.json` para `pnpm-lock.yaml`
- Atualização do ESLint (`@typescript-eslint` v7 → v8)

## Checklist de revisão

### Antes do merge

- [ ] Revisar os arquivos alterados
- [ ] Confirmar que o `pnpm install` roda sem erros
- [ ] Rodar os testes (`pnpm test`)
- [ ] Rodar o lint (`pnpm run lint`)
- [ ] Rodar o typecheck (`pnpm run typecheck`)
- [ ] Confirmar que a aplicação sobe (`pnpm dev`)

### Deploy

- [ ] Build de produção OK (`pnpm build`)
- [ ] Deploy realizado no servidor
- [ ] Aplicação respondendo após o deploy
- [ ] Logs sem erro

### Depois do merge

- [ ] Tag de release criada
- [ ] Branch `develop` sincronizada com a `main`
