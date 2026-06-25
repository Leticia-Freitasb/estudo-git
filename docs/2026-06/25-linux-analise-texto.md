# Estudos da Lele 🌸
 
💖 Errar é o feitiço; persistir é a magia — Diário de uma Iniciante 🌸
 
Resumo dos estudos do dia — **Linux: análise de texto na prática**.
Data: 25 de junho de 2026
 
> Hoje aprendi a fatiar e resumir dados direto no terminal.
 
## 📄 Espiando arquivos (head e tail)
 
- **`head -3 arquivo`** — mostra as primeiras 3 linhas
- **`tail -2 arquivo`** — mostra as últimas 2 linhas
- Ótimos pra espiar arquivos grandes sem abrir tudo
## 🔤 Ordenar com sort
 
- **`sort arquivo`** — ordena as linhas (alfabético por padrão)
- **`sort -r arquivo`** — ordena ao contrário (Z → A)
## ✂️ Recortar colunas com cut
 
- **`cut -d"," -f1 arquivo`** — extrai a coluna 1 de um arquivo separado por vírgula
- `-d","` define o separador (delimitador); `-f` escolhe o campo (field)
- Ex.: `-f3` pega a terceira coluna
## 🧹 Remover e contar repetições (uniq)
 
- **`uniq`** — remove linhas repetidas que estão lado a lado
- Por isso a gente **ordena antes** (`sort | uniq`), pra agrupar as iguais
- **`uniq -c`** — conta quantas vezes cada linha aparece
## 🔗 Combinando tudo com pipe
 
- Lista de cidades sem repetir, em ordem:
```bash
  cut -d"," -f3 pessoas.csv | sort | uniq
```
- Quantas pessoas em cada cidade:
```bash
  cut -d"," -f3 pessoas.csv | sort | uniq -c
```
- Análise de dados de verdade, só com comandos pequenos encadeados!
## 🔎 Buscar e contar com grep
 
- **`grep "Recife" arquivo | wc -l`** — conta as linhas que têm "Recife"
- **`grep -c "Recife" arquivo`** — atalho do grep que já conta direto (sem pipe)
## 🤖 Script de relatório
 
- Criei um `relatorio.sh` que gera um resumo automático dos dados:
```bash
  #!/bin/bash
  echo "=== Relatório de Pessoas ==="
  echo "Total de pessoas:"
  cat pessoas.csv | wc -l
  echo "Cidades (sem repetir):"
  cut -d"," -f3 pessoas.csv | sort | uniq
  echo "Pessoas por cidade:"
  cut -d"," -f3 pessoas.csv | sort | uniq -c
```
- `chmod +x relatorio.sh` e `./relatorio.sh` pra rodar
## 💡 Conceitos que fixei
 
- `head` e `tail` mostram começo e fim de um arquivo
- `sort` ordena; `-r` inverte a ordem
- `cut` recorta colunas usando um delimitador
- `uniq` só remove repetidas que estão juntas, por isso `sort` vem antes
- `uniq -c` conta repetições — vira análise de dados
- O pipe `|` encadeia ferramentas pequenas pra resolver coisas grandes
## ✨ Destaque do dia
 
Fiz minha primeira **análise de dados no terminal**: a partir de um arquivo CSV,
descobri quantas pessoas há em cada cidade usando `cut | sort | uniq -c`. 🎉
 
## 🧪 Quer praticar junto? Todos os comandos do dia
 
Se você está começando igual eu comecei, é só copiar e rodar na ordem. 🌸
 
```bash
# Preparar o terreno
cd ~
mkdir treino-linux-2 && cd treino-linux-2
 
# Criar um arquivo de dados (nome, idade, cidade)
printf "Ana,28,Recife\nBruno,35,Salvador\nCarla,22,Recife\nDiego,41,Manaus\nElena,30,Salvador\nFabio,19,Recife\n" > pessoas.csv
cat pessoas.csv
 
# 1. Espiar começo e fim
head -3 pessoas.csv
tail -2 pessoas.csv
 
# 2. Ordenar
sort pessoas.csv
sort -r pessoas.csv
 
# 3. Recortar colunas (cut)
cut -d"," -f1 pessoas.csv     # nomes
cut -d"," -f3 pessoas.csv     # cidades
 
# 4. Cidades sem repetir, em ordem
cut -d"," -f3 pessoas.csv | sort | uniq
 
# 5. Contar pessoas por cidade
cut -d"," -f3 pessoas.csv | sort | uniq -c
 
# 6. Buscar e contar com grep
grep "Recife" pessoas.csv | wc -l
grep -c "Recife" pessoas.csv
 
# 7. Criar o script de relatório
nano relatorio.sh    # cole o conteúdo do script, salve com Ctrl+O, Enter, Ctrl+X
chmod +x relatorio.sh
./relatorio.sh
```
 
> 💡 **Dicas de quem tropeçou primeiro:**
> - No `cut`, não esqueça o `-d` pra dizer qual é o separador.
> - O `uniq` só junta repetidas que estão lado a lado — sempre `sort` antes.
> - `grep -c` já conta; não precisa do `| wc -l` junto.
 
## 🚀 Próximos passos
 
- Usar variáveis dentro de scripts
- Fazer o script tomar decisões com `if`
- Repetir tarefas com loops (`for`)
