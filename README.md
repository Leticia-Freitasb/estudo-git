# Git e GitHub do Zero — Diário de uma Iniciante 🌸

Este é o meu passo a passo de quando aprendi Git e GitHub **começando do absoluto zero**.
Escrevi do jeito que eu queria ter encontrado quando comecei: com os erros incluídos,
porque é tropeçando que a gente aprende de verdade.

Se você está começando agora, respira fundo: **todo erro aqui embaixo eu cometi de verdade**.
Faz parte. Bora.

---

## Índice

1. [O que é cada coisa (em 1 minuto)](#o-que-é-cada-coisa)
2. [Parte 1 — O `.gitignore`](#parte-1--o-gitignore)
3. [Parte 2 — O fluxo branch → edita → merge](#parte-2--o-fluxo-branch--edita--merge)
4. [Parte 3 — Publicar no GitHub](#parte-3--publicar-no-github)
5. [Os erros que eu cometi (e como escapei)](#os-erros-que-eu-cometi)
6. [Colinha de comandos](#colinha-de-comandos)

---

## O que é cada coisa

Antes de tudo, pra não ficar perdida:

- **Git** → o programa que roda no seu computador e guarda o histórico do seu projeto.
  Pensa nele como um "salvar com histórico": cada vez que você salva (um *commit*),
  ele guarda uma foto do projeto naquele momento.
- **GitHub** → um site na nuvem onde você guarda uma cópia dos seus projetos Git.
  É tipo o Google Drive do Git: backup + lugar pra mostrar o que você fez pro mundo.
- **Repositório (repo)** → a pasta do seu projeto que o Git está vigiando.
- **Commit** → uma "foto" salva do projeto, com uma mensagem dizendo o que mudou.
- **Branch** → uma linha de trabalho paralela. Você experimenta nela sem bagunçar a principal.

---

## Parte 1 — O `.gitignore`

O `.gitignore` é um arquivo de texto que diz ao Git **o que ele deve IGNORAR**.
Coisas que não fazem sentido guardar: senhas, arquivos temporários, pastas de
dependências baixadas, etc.

### Criando o repositório

```bash
mkdir estudo-git && cd estudo-git
git init
```

- `mkdir estudo-git` → cria a pasta. (Atenção: é `mkdir`, com UM "d" só!)
- `&&` → "e depois faça isto também".
- `cd estudo-git` → entra na pasta.
- `git init` → liga o Git ali dentro. A partir daqui o Git vigia essa pasta.

### Criando o arquivo `.gitignore`

O jeito mais simples é com o editor `nano`:

```bash
nano .gitignore
```

Aí você digita o conteúdo (cada linha é um padrão):

```gitignore
# Linhas começando com # são comentários

config.secret      # ignora este arquivo específico
*.log              # ignora TODOS os arquivos terminados em .log
node_modules/      # ignora uma pasta inteira (a / indica pasta)
.env               # ignora arquivos de ambiente (senhas, chaves)
```

Pra salvar e sair do nano:
- `Ctrl + O` → salva (de "Output")
- `Enter` → confirma o nome
- `Ctrl + X` → sai

> ⚠️ **A maior confusão da minha vida aqui:** o conteúdo do `.gitignore` vai
> DENTRO do arquivo. Não digite essas linhas direto no terminal! Se você digitar
> `*.log` no terminal, ele vai responder `command not found`, porque ele acha que
> você quer rodar um programa chamado "*.log". Essas linhas são CONTEÚDO, não comandos.

### Testando se funciona

```bash
echo "segredo" > config.secret
echo "log qualquer" > app.log
git status
```

Se deu certo, o `git status` mostra **só** o `.gitignore` — o `config.secret` e o
`app.log` não aparecem, porque estão sendo ignorados. 🎉

> 💡 **Pegadinha importante:** o `.gitignore` só funciona em arquivos que o Git
> ainda NÃO está rastreando. Se você já deu `git add` num arquivo antes de
> ignorá-lo, tem que tirar do rastreamento com:
> ```bash
> git rm --cached nome-do-arquivo
> ```

### Primeiro commit

```bash
git add .
git commit -m "primeiro commit: adiciona .gitignore"
```

- `git add .` → coloca tudo na "área de preparação" (o ponto `.` significa "tudo").
- `git commit -m "..."` → grava a foto, com a mensagem entre aspas.

Na primeira vez, o Git pode pedir pra você se identificar. Configure assim
(com SEUS dados):

```bash
git config --global user.name "Seu Nome"
git config --global user.email "seu@email.com"
```

Pra conferir:

```bash
git config --global --list
```

---

## Parte 2 — O fluxo branch → edita → merge

Esse é o coração do trabalho do dia a dia. A regra de ouro:
**você nunca mexe direto na branch principal.** Pra cada tarefa nova, cria uma
branch, trabalha nela, e depois junta de volta.

### Passo 1 — Criar uma branch e entrar nela

```bash
git checkout -b nova-funcionalidade
```

- `-b` → "crie a branch E já me leve pra ela". (É `-b` grudado, sem espaço!)

Confira onde você está:

```bash
git branch
```

O `*` marca a branch atual. O próprio terminal também mostra o nome da branch
no prompt — fica de olho nisso.

### Passo 2 — Editar e commitar nessa branch

```bash
echo "Linha criada na branch nova!" >> README.md
git add README.md
git commit -m "adiciona linha na nova funcionalidade"
```

> ⚠️ **Atenção ao `>>`:** são DUAS setas, que ACRESCENTAM ao arquivo.
> Uma seta só (`>`) APAGA tudo e sobrescreve. Pra não perder conteúdo, use `>>`.

### Passo 3 — O momento mágico ✨

Volte pra principal e olhe o arquivo:

```bash
git checkout master
cat README.md
```

A linha que você criou **NÃO vai estar lá** (ou o arquivo nem existe ainda).
Por quê? Porque ela vive só na outra branch! As branches são realidades paralelas.
Esse é o momento em que o conceito "clica": você pode quebrar tudo numa branch
sem afetar a principal.

### Passo 4 — Merge (trazendo o trabalho de volta)

Estando na branch principal:

```bash
git merge nova-funcionalidade
cat README.md
```

Agora a linha aparece! O trabalho voltou pra casa. Se a principal não mudou nesse
meio-tempo, o Git faz um merge tranquilo chamado *Fast-forward*.

### Passo 5 — Limpar a branch usada

```bash
git branch -d nova-funcionalidade
```

- `-d` → apaga a branch (só funciona se ela já foi mesclada — é uma trava de segurança boa).

### O ciclo completo (decore isto!)

```bash
git checkout -b minha-tarefa    # 1. cria e entra na branch
# ...edita arquivos...
git add .                       # 2. prepara
git commit -m "o que mudei"     #    grava
git checkout master             # 3. volta pra principal
git merge minha-tarefa          # 4. junta o trabalho
git branch -d minha-tarefa      # 5. limpa
```

Isso é literalmente o que se faz TODO DIA trabalhando com Git.

---

## Parte 3 — Publicar no GitHub

Agora vamos mandar o repositório local pra nuvem.

### Etapa 1 — Criar o repositório vazio no site

1. Entre em [github.com](https://github.com) e faça login.
2. Clique no **`+`** no canto superior direito → **New repository**.
3. Dê um nome (ex: `estudo-git`).
4. **NÃO marque** as caixas de README, `.gitignore` ou license — você já tem
   tudo isso no local, e isso evita conflito.
5. Clique em **Create repository**.

### Etapa 2 — Conectar e enviar

Troque `SEU-USUARIO` pelo seu nome de usuário do GitHub:

```bash
git remote add origin https://github.com/SEU-USUARIO/estudo-git.git
git branch -M main
git push -u origin main
```

- `git remote add origin ...` → conecta o local ao repositório da nuvem
  (`origin` é só o apelido padrão do remoto).
- `git branch -M main` → renomeia a branch de `master` pra `main`
  (o GitHub usa `main` como padrão hoje).
- `git push -u origin main` → ENVIA seus commits pra nuvem.
  O `-u` cria o vínculo, então das próximas vezes basta `git push`.

### Etapa 3 — Autenticação (o ponto que mais trava!)

O GitHub **não aceita mais a senha da conta** no push. Você precisa de um
**Personal Access Token** (uma senha descartável só pra isso).

Como gerar:
1. No GitHub: sua foto → **Settings**.
2. No final do menu esquerdo → **Developer settings**.
3. **Personal access tokens** → **Tokens (classic)** → **Generate new token (classic)**.
4. Dê um nome, escolha a validade, e marque a caixa **`repo`** (essa é a permissão essencial).
5. **Generate token** lá embaixo.
6. Copie o código `ghp_...` na hora — **ele só aparece UMA vez!**

Quando o terminal pedir no push:
- **Username:** seu usuário do GitHub.
- **Password:** cole o **TOKEN** (não a senha da conta!).

> 🚨 **O SUSTO QUE EU TOMEI:** quando você cola o token na senha, a tela
> **NÃO MOSTRA NADA** — nem bolinha, nem asterisco, nem o cursor mexe. Parece
> que travou. **NÃO TRAVOU!** É proteção do terminal. Cole e dê Enter "no escuro",
> confiando. Eu achei que tinha travado e quase surtei. Não trava. 😅
>
> Dica: pra colar no terminal, use **botão direito do mouse → Paste**, ou
> `Ctrl+Shift+V`. O `Ctrl+V` comum às vezes não funciona em terminal.

Se deu certo, você vê:

```
* [new branch]      main -> main
branch 'main' set up to track 'origin/main'.
```

🎉 **Seus arquivos estão na nuvem!** Abra `https://github.com/SEU-USUARIO/estudo-git`
no navegador pra ver.

---

## Os erros que eu cometi

Coloquei todos aqui porque foi com eles que eu mais aprendi. Se acontecer com você,
não é burrice — é rito de passagem. 😄

| O que eu fiz de errado | O que aconteceu | A correção |
|---|---|---|
| Digitei `mkddir` (dois "d") | `command not found` | É `mkdir`, com um "d" só |
| Digitei o conteúdo do `.gitignore` no terminal | `command not found` em cada linha | Conteúdo vai DENTRO do arquivo, não no terminal |
| `git config user .email` (espaço) | `command not found` | É `user.email`, tudo grudado |
| `"git config...` (aspa solta no começo) | comando se perdeu | A aspa só envolve o VALOR, não o comando todo |
| `git checkout - b` (espaço no `-b`) | apareceu o texto de ajuda | É `-b` grudado |
| Aspa aberta e não fechada | apareceu uma bolinha `•` esperando | `Ctrl+C` pra cancelar e recomeçar |
| Achei que o terminal travou na senha | a tela não mostrava nada | É proteção; a senha é invisível de propósito |

### Atalhos de terminal que salvam vidas

- **`Ctrl + C`** → cancela o que está rodando / sai de uma linha bagunçada. Seu botão de pânico.
- **Seta pra cima ↑** → recupera o último comando, pra não redigitar tudo.
- **Botão direito → Paste** (ou `Ctrl+Shift+V`) → cola no terminal.

### A regra de ouro do terminal

**O terminal é radical com espaços.** Onde tem espaço, ele corta e trata como
coisas separadas. Por isso `user.email`, `-b`, `-m` andam todos GRUDADOS,
sem espaço no meio. A maioria dos meus erros foi espaço no lugar errado.

---

## Colinha de comandos

```bash
# --- Começar um projeto ---
git init                          # liga o Git na pasta
git status                        # mostra o que mudou

# --- Salvar trabalho ---
git add .                         # prepara tudo
git commit -m "mensagem"          # grava a foto

# --- Branches (trabalho paralelo) ---
git checkout -b nome              # cria e entra numa branch
git branch                        # lista as branches (* = atual)
git checkout main                 # troca de branch
git merge nome                    # junta uma branch na atual
git branch -d nome                # apaga uma branch já mesclada

# --- GitHub (nuvem) ---
git remote add origin URL         # conecta ao repositório remoto
git push                          # envia pra nuvem
git pull                          # traz da nuvem pro local

# --- Configuração (uma vez só) ---
git config --global user.name "Seu Nome"
git config --global user.email "seu@email.com"
git config --global --list        # confere a config
```

---

## Próximos passos (pra quando eu evoluir)

- **Conflitos de merge** — quando duas branches editam a mesma linha. Parece
  assustador mas não é bicho de sete cabeças.
- **`git pull`** — trazer mudanças da nuvem de volta pro computador.
- **Pull requests** — o jeito "social" de propor mudanças em projetos no GitHub.

---

*Escrito por alguém que começou do zero. Se eu consegui, você também consegue. 🌸*
