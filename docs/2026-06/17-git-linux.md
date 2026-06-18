💖 Errar é o feitiço; persistir é a magia — Diário de uma Iniciante 🌸


Resumo dos estudos do dia — **Git & Linux na prática**.
Data: 17 de junho de 2026

## 🌿 Git — controle de versão

- Instalei o Git e configurei minha identidade (`git config` com nome e e-mail)
- Aprendi o ciclo de trabalho: `init` → `add` → `commit` → `log`
- Usei `git status` para acompanhar o que mudou a cada etapa
- Criei e naveguei entre **branches** (`checkout -b`) e fiz **merge**
- Entendi a lógica de branches como "linhas paralelas" de trabalho

## ⚔️ Conflito de merge

- Provoquei um conflito de propósito editando a mesma linha em duas branches
- Interpretei as marcações do Git (`<<<`, `===`, `>>>`)
- Escolhi a versão correta e **resolvi o conflito** manualmente
- Finalizei com `git add` + `git commit` para encerrar o merge

## 💻 Comandos Linux

- Navegação e listagem: `pwd`, `ls`, `ls -l`, `cd`
- Arquivos e pastas: `mkdir`, `touch`, `cp`, `mv`, `rm`, `cat`
- Edição de arquivos pelo terminal com o editor **nano**
- Entendi `>` (sobrescreve) vs `>>` (acrescenta)

## 🔐 Permissões de arquivos

- Usei `chmod +x` para tornar um script executável
- Entendi a notação **rwx** (ler, escrever, executar)
- Aprendi a notação numérica: **r=4, w=2, x=1**
- Pratiquei conversões: `755` = `rwxr-xr-x` e `644` = `rw-r--r--`
- Criei e executei meu próprio script `.sh`

## 🪄 Ambiente & configuração

- Configurei o WSL (Ubuntu rodando dentro do Windows)
- Personalizei o terminal editando o `.bashrc`
- Criei mensagem de boas-vindas e usei **pipe** (`|`) com figlet e lolcat
- Editei o prompt (Starship) escrevendo um arquivo de config pelo terminal

## 💡 Conceitos que fixei

- Linux é **case sensitive** (diferencia maiúsculas de minúsculas)
- Windows e WSL têm sistemas de arquivos **separados**
- Como ler mensagens de erro comuns (ex.: `No such file or directory`)
- A importância de conferir o estado antes de agir (`ls`, `git status`, `cat`)

## ✨ Destaque do dia

Resolvi com sucesso meu **primeiro conflito de merge no Git** — do começo (provocar o conflito) ao fim (escolher a versão certa e finalizar). 🎉

## 🚀 Próximos passos

- Publicar um repositório no GitHub
- Praticar o fluxo: branch → edita → merge no dia a dia
- Aprender o `.gitignore`
