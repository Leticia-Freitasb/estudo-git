# Estudos da Lele 🌸
 
💖 Errar é o feitiço; persistir é a magia — Diário de uma Iniciante 🌸
 
Resumo dos estudos do dia — **Linux intermediário na prática**.
Data: 23 de junho de 2026
 
> Voltei depois de uns dias doente — o diário espera a gente. 💪
 
## 🗂️ Criando estruturas de pastas
 
- Criei várias pastas de uma vez com chaves: `mkdir -p projeto/{src,docs,testes}`
- Entendi que o `-p` cria pastas aninhadas e **não reclama** se a pasta já existe
- Visualizei estruturas com `ls -R` (mostra tudo, em todos os níveis)
## 🔍 Buscar conteúdo e arquivos
 
- **`grep`** — procura um texto **dentro** de arquivos (ex.: `grep "abacaxi" frutas.txt`)
- **`find`** — procura arquivos e pastas por nome (ex.: `find . -name "*.py"`)
- `find . -type d` — lista **todas as pastas** a partir de um ponto
## 🔗 Pipe `|` — encadeando comandos
 
- Aprendi o **pipe `|`**: pega o resultado de um comando e entrega pro próximo
- `cat frutas.txt | wc -l` → conta as linhas do arquivo
- `cat frutas.txt | grep "a" | wc -l` → dois pipes em sequência (filtra e conta)
- Entendi que o `|` é como uma "esteira" que liga ferramentas pequenas
## 🧮 Contar e inspecionar
 
- **`wc -l`** — conta o número de linhas (de "lines")
- **`cat -n`** — mostra o conteúdo com as linhas **numeradas**
- Descobri a pegadinha: `wc -l` conta quebras de linha, então a última linha
  sem "Enter" não entra na conta
- Lição de ouro: **o número engana; sempre vale olhar o conteúdo de verdade**
## 🌳 Visualizar a estrutura com `tree`
 
- Instalei o `tree` com `sudo apt install tree`
- `tree` — desenha a árvore de pastas e arquivos de forma visual
- `tree -d` — mostra só as pastas (sem os arquivos)
## 📦 Reorganizar com `mv`
 
- Usei o `mv` pra **mover pastas inteiras** de um lugar pro outro
- Ex.: `mv projeto/git aulas/` (joga a pasta `git` pra dentro de `aulas`)
- Confirmei o antes e o depois com `tree -d`
## 🤖 Meu primeiro script de automação
 
- Criei um script `relatorio.sh` que junta vários comandos:
```bash
  #!/bin/bash
  echo "=== Estrutura do treino ==="
  tree -d
  echo ""
  echo "Total de pastas:"
  find . -type d | wc -l
```
- Dei permissão de execução com `chmod +x relatorio.sh`
- Executei com `./relatorio.sh`
- Entendi que script é **automação**: empacotar tarefas repetidas num comando só
## 💡 Conceitos que fixei
 
- O Linux é literal: `wc -l` conta linhas de verdade, não "intenções"
- Investigar com `cat -n` revela o que um número sozinho esconde
- O pipe `|` encadeia ferramentas pequenas pra resolver coisas grandes
- `mv` serve tanto pra mover quanto pra renomear
- Um `.sh` + `chmod +x` transforma uma sequência de comandos num programinha
## ✨ Destaque do dia
 
Escrevi e executei meu **primeiro script de automação** (`.sh`) — juntando `tree`,
`find` e pipe num programa só, com permissão de execução e tudo. 🎉
 
## 🚀 Próximos passos
 
- Aprender `sort` (ordenar), `head` e `tail` (ver começo/fim de arquivos)
- Usar variáveis dentro de scripts
- Fazer o script tomar decisões com `if`
---
 
## 🧪 Quer praticar junto? Todos os comandos do dia
 
Se você está começando igual eu comecei, é só copiar e rodar na ordem.
Faça num lugar de teste pra não bagunçar nada importante. Bora! 🌸
 
```bash
# 1. Criar uma pasta de treino e entrar nela
cd ~
mkdir treino-linux && cd treino-linux
 
# 2. Criar várias pastas de uma vez (chaves criam todas juntas)
mkdir -p projeto/{src,docs,testes}
ls -R projeto                       # mostra a pasta e tudo dentro dela
 
# 3. Criar arquivos vazios e escrever conteúdo
touch projeto/src/main.py projeto/src/util.py projeto/docs/leiame.txt
echo "print('Olá Linux')" > projeto/src/main.py
cat projeto/src/main.py             # mostra o conteúdo do arquivo
 
# 4. Criar um arquivo com várias linhas (uma fruta por linha)
printf "maçã\nbanana\nabacaxi\nmanga\nmelancia\n" > projeto/docs/frutas.txt
cat -n projeto/docs/frutas.txt      # mostra com as linhas numeradas
 
# 5. Buscar TEXTO dentro de um arquivo (grep)
grep "abacaxi" projeto/docs/frutas.txt
 
# 6. Buscar ARQUIVOS por nome (find) — o * é curinga
find projeto -name "*.py"
 
# 7. Copiar, mover e renomear
cp projeto/docs/leiame.txt projeto/docs/leiame-copia.txt
mv projeto/docs/leiame-copia.txt projeto/docs/backup.txt
 
# 8. Pipe | — liga um comando no outro como uma esteira
cat projeto/docs/frutas.txt | wc -l              # conta as linhas
cat projeto/docs/frutas.txt | grep "a" | wc -l   # filtra com "a" e conta
 
# 9. Ver a estrutura de pastas de forma visual (tree)
sudo apt install tree    # instala (só na primeira vez)
tree                     # árvore com pastas e arquivos
tree -d                  # só as pastas
 
# 10. Listar todas as pastas a partir daqui
find . -type d
 
# 11. Criar e rodar um script de automação
nano relatorio.sh        # cole o conteúdo abaixo, salve com Ctrl+O, Enter, Ctrl+X
```
 
Conteúdo do `relatorio.sh`:
 
```bash
#!/bin/bash
echo "=== Estrutura do treino ==="
tree -d
echo ""
echo "Total de pastas:"
find . -type d | wc -l
```
 
Depois de salvar o script:
 
```bash
chmod +x relatorio.sh    # dá permissão de execução (o x das permissões)
./relatorio.sh           # roda o script (o ./ = "execute este daqui")
```
 
> 💡 **Dicas de quem tropeçou primeiro:**
> - Cuidado com `-l` (letra L) vs `-1` (número um): no `wc -l` é a **letra**.
> - `>` sobrescreve o arquivo; `>>` acrescenta no final. Não confunda!
> - O número que o `wc -l` mostra pode enganar — sempre confira com `cat -n`.
> - Se um comando "travar" esperando, `Ctrl+C` cancela e recomeça.
