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
| `git branch -r` | Lista só as branches remotas |
| `git branch -v` | Lista mostrando o último commit de cada branch |
| `git branch -vv` | Lista mostrando também o vínculo com o remoto (upstream) |
| `git branch --merged` | Lista as branches já mergeadas na branch atual |
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

## Git — Remotes (repositórios remotos)

| Comando | O que faz |
|---|---|
| `git remote -v` | Lista os remotes configurados (fetch e push) |
| `git remote add origin url-do-repo` | Adiciona um remote chamado `origin` |
| `git remote rename origin upstream` | Renomeia o remote `origin` para `upstream` |
| `git remote set-url origin nova-url` | Troca a URL de um remote |
| `git remote remove nome-do-remote` | Remove um remote |
| `git fetch upstream` | Baixa as atualizações do repo original (sem mesclar) |
| `git push origin --all` | Envia **todas** as branches locais |
| `git push origin --tags` | Envia todas as tags |

### Diferença entre `origin` e `upstream`

| Remote | Aponta para | Serve pra |
|---|---|---|
| `origin` | Seu fork (`LucasCastro100/b7cicd-example`) | Enviar seu código (push) ✅ |
| `upstream` | Repo original (`suporteb7web/b7cicd-example`) | Puxar atualizações do curso |

## Git — Fork (contribuir num repo que você não tem permissão)

Clonar só precisa de **leitura**. Dar **push** exige permissão de **escrita**.
Se você não for colaborador, faça um **fork** (cópia na sua conta) e faça push lá.

```bash
# 1. Cria o fork na sua conta (precisa do gh autenticado)
gh repo fork suporteb7web/b7cicd-example --clone=false

# 2. Ajusta os remotes: origin = seu fork, upstream = repo original
git remote rename origin upstream
git remote add origin https://github.com/LucasCastro100/b7cicd-example.git

# 3. Confere se ficou certo
git remote -v

# 4. Envia a branch para o seu fork
git push -u origin feature/test
```

Sem o `gh`, faça o fork pelo site (botão **Fork**) e depois só troque a URL:

```bash
git remote set-url origin https://github.com/SEU_USUARIO/b7cicd-example.git
git push -u origin feature/test
```

## Git — Pull Request (GitHub CLI)

O `gh` é a ferramenta oficial do GitHub no terminal. Instale e autentique:

```bash
brew install gh
gh auth login      # só na primeira vez
gh auth status     # confere a conta logada
```

| Comando | O que faz |
|---|---|
| `gh pr create` | Cria o pull request (modo interativo) |
| `gh pr create --base main --head usuario:branch` | Cria o PR direto com parâmetros |
| `gh pr list` | Lista os PRs abertos |
| `gh pr view` | Mostra o PR da branch atual |
| `gh pr view --web` | Abre o PR no navegador |
| `gh pr checks` | Mostra o status dos testes/CI do PR |
| `gh pr merge` | Faz o merge do PR |
| `gh pr merge --squash --delete-branch` | Merge com squash e apaga a branch |
| `gh pr close` | Fecha o PR sem fazer merge |
| `gh repo fork repo-do-upstream` | Cria um fork na sua conta |

### Exemplo de PR do seu fork para o repo original

```bash
gh pr create \
  --repo suporteb7web/b7cicd-example \
  --base main \
  --head LucasCastro100:feature/test \
  --title "feat: arquivos básicos de alteração" \
  --body "Descrição do que foi feito"
```

O `--head LucasCastro100:feature/test` diz que o PR vem **do seu fork**.

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

## Git — Fluxo real usado no projeto (enviar branch e mesclar na develop)

Passo a passo do que foi feito para enviar a `develop` e mesclar a `feature/test` nela.

### 1. Ver o estado das branches

```bash
git branch -vv          # branches locais + vínculo com o remoto
git branch -r           # branches remotas
git log develop --oneline -3   # últimos commits da develop
```

### 2. Enviar a `develop` para o seu fork

```bash
git push -u origin develop
```

O `-u` vincula a branch local à remota — depois disso, nos próximos pushes basta `git push`.

### 3. Mesclar a `feature/test` na `develop`

```bash
git switch develop
git merge feature/test --no-ff -m "merge: traz alterações da feature/test para develop"
git push
```

| Comando | O que faz |
|---|---|
| `git switch develop` | Troca para a branch `develop` |
| `git merge feature/test --no-ff` | Mescla a `feature/test` na atual, forçando um commit de merge |
| `-m "..."` | Define a mensagem do commit de merge |
| `git push` | Envia a `develop` atualizada para o seu fork |

### 4. Ver o histórico em grafo

```bash
git log --oneline --graph --all -8
```

O histórico em grafo mostra o commit de merge e as branches se juntando:

```
*   7f50880 merge: traz alterações da feature/test para develop
|\
| * eaa36cd docs: adiciona comandos...
| * 08cdecd feat: subindo arquivos básicos...
|/
* 963cf0b initial commit
```
