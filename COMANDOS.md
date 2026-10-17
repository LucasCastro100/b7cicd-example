# Comandos do Projeto

> Gerenciador de pacotes: **pnpm**

## Aplicação

| Comando | O que faz |
|---|---|
| `pnpm start` | Compila e sobe a aplicação |
| `pnpm run dev` | Sobe em modo watch (sem precisar compilar) |
| `pnpm run build` | Compila o TypeScript para a pasta `dist/` |
| `pnpm test` | Roda os testes |
| `pnpm run lint` | Verifica o código com ESLint |
| `pnpm run typecheck` | Verifica os tipos sem compilar (`tsc --noEmit`) |

## Git — Status e histórico

| Comando | O que faz |
|---|---|
| `git status` | Mostra o estado atual dos arquivos |
| `git log --oneline` | Lista os commits de forma resumida |
| `git log --oneline --graph --all` | Mostra o histórico em grafo (todas as branches) |
| `git diff` | Mostra as alterações ainda não adicionadas |
| `git diff --staged` | Mostra as alterações já adicionadas (staged) |

## Git — Branches

| Comando | O que faz |
|---|---|
| `git branch` | Lista as branches locais |
| `git branch -a` | Lista as branches locais e remotas |
| `git switch -c nome-da-branch` | Cria **e** troca para a nova branch |
| `git checkout -b nome-da-branch` | Forma antiga de criar e trocar de branch |
| `git branch nome-da-branch` | Cria a branch **sem** trocar para ela |
| `git switch nome-da-branch` | Troca para uma branch existente |
| `git branch -d nome-da-branch` | Deleta uma branch (se já foi mergeada) |
| `git branch -D nome-da-branch` | Força a deleção de uma branch |

## Git — Salvar alterações

| Comando | O que faz |
|---|---|
| `git add .` | Adiciona todas as alterações para o próximo commit |
| `git add arquivo.ts` | Adiciona um arquivo específico |
| `git commit -m "mensagem"` | Cria um commit com as alterações adicionadas |
| `git push` | Envia os commits para o repositório remoto |
| `git push -u origin nome-da-branch` | Envia a branch e define o upstream |
| `git pull` | Baixa e mescla as alterações do remoto |

## Git — Merge

| Comando | O que faz |
|---|---|
| `git switch main` | Vai para a branch de destino (ex.: `main`) |
| `git merge nome-da-branch` | Mescla outra branch na atual |
| `git merge --no-ff nome-da-branch` | Mescla criando sempre um commit de merge |
| `git merge --abort` | Cancela um merge que deu conflito |
| `git rebase main` | Reaplica os commits da branch atual sobre a `main` |

## Git — Desfazer alterações

| Comando | O que faz |
|---|---|
| `git restore arquivo.ts` | Descarta alterações de um arquivo (não staged) |
| `git restore --staged arquivo.ts` | Remove um arquivo da área de stage |
| `git reset --soft HEAD~1` | Desfaz o último commit, mantendo as alterações |
| `git reset --hard HEAD~1` | Desfaz o último commit e descarta as alterações |
| `git stash` | Guarda alterações temporariamente |
| `git stash pop` | Recupera as alterações guardadas com o stash |

## Git — Fluxo comum (criar branch, commitar e mergear)

```bash
# 1. Cria e entra numa nova branch
git switch -c feature/minha-feature

# 2. Salva as alterações
git add .
git commit -m "feat: adiciona minha feature"

# 3. Envia para o remoto
git push -u origin feature/minha-feature

# 4. Volta para a main e mescla
git switch main
git pull
git merge feature/minha-feature
git push
```
