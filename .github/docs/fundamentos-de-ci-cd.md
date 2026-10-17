# Fundamentos de CI/CD

Este documento resume os conceitos fundamentais sobre a estrutura e o funcionamento de um **Pipeline de CI/CD**.

---

## Conceitos-chave

* **Trigger (gatilho):** evento que dispara a execução automática do pipeline (ex.: um `push` na branch, a abertura de um *Pull Request*, um agendamento de horário etc.).
* **Job (trabalho/etapa):** conjunto de tarefas (*steps*) que executam em um determinado ambiente ou contêiner. Em um pipeline, múltiplos *jobs* podem rodar em sequência ou em paralelo.
* **Step (passo/instrução):** cada um dos comandos individuais executados dentro de um *job*.
* **Artifact (artefato):** arquivos gerados durante a execução de um *job* (como a pasta de compilação `dist/`) que precisam ser salvos ou transferidos para outros *jobs* posteriores (como o de *deploy*).

---

## Fluxo e estrutura do pipeline

Divisão prática das fases (*jobs*) do pipeline:

```
[ Trigger / Gatilho ]
       │
       ├─► Job: test
       │     ├─ checkout/switch
       │     ├─ pnpm install
       │     └─ pnpm test
       │
       ├─► Job: build
       │     ├─ checkout/switch
       │     ├─ pnpm install
       │     ├─ pnpm run build
       │     └─ salvar dist/ ──► ( Artifact )
       │                               │
       └─► Job: deploy ◄───────────────┘
             ├─ baixar artifact
             ├─ enviar por SSH
             └─ restart app
```

---

## Detalhamento dos jobs

### 1. Job: `test`

Responsável por garantir a qualidade e o funcionamento das alterações no código antes do build.

* **`checkout/switch`**: baixa o código-fonte da branch/repositório.
* **`pnpm install`**: instala as dependências do projeto.
* **`pnpm test`**: executa a suíte de testes automatizados.

---

### 2. Job: `build`

Responsável por compilar/empacotar a aplicação para produção.

* **`checkout/switch`**: baixa o código-fonte.
* **`pnpm install`**: instala as dependências necessárias.
* **`pnpm run build`**: gera os arquivos otimizados para produção.
* **`salvar dist/`**: armazena o resultado da compilação como um **artifact** para ser reutilizado.

---

### 3. Job: `deploy`

Responsável por publicar a aplicação compilada no servidor de destino.

* **`baixar artifact`**: obtém o arquivo de build (`dist/`) salvo no job anterior.
* **`enviar via SSH`**: transfere os arquivos para o servidor de produção/staging.
* **`restart app`**: reinicia o serviço/aplicação para que as alterações fiquem ativas.
