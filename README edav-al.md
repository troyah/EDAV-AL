# EDAV-AL: corpus textual para análise lexicométrica dos itens

Este repositório reúne o material que preparei para a análise semântica e lexical dos itens do instrumento **EDAV-AL**, usando o **IRAMUTEQ** como ponte lexicométrica.

O objetivo é verificar a **validade de conteúdo** e a **estrutura semântica** dos itens, ou seja, mapear se o texto escrito reflete as dimensões teóricas do instrumento. Também quero comparar as 5 versões do instrumento entre si.

## Dimensões teóricas

| Código no corpus | Dimensão |
|---|---|
| `dim_1_hipervigilancia` | Hipervigilância Social e Adaptativa |
| `dim_2_carga_mental` | Carga Mental de Transposição de Barreiras |
| `dim_3_agencia_comunitaria` | Agência Comunitária e Rede de Cuidado Solidário |
| `dim_4_pertencimento` | Sentimento de Pertencimento e Desalienação do Espaço |
| `dim_5_saude_mental` | Preservação da Saúde Mental e Suporte Psíquico no Trabalho (aparece só na v2) |

## Estrutura do repositório

| Arquivo | Conteúdo |
|---|---|
| `corpus_v1.txt` a `corpus_v5.txt` | Um corpus por versão do instrumento, para análise separada |
| `corpus_combinado.txt` | As 5 versões juntas (205 itens), com a variável `*vN` no cabeçalho |
| `build_corpus.py` | Script que gera todos os corpus a partir dos itens |

## Formato do corpus

Cada item é uma unidade de texto com uma linha de comandos (iniciada por `****`) seguida do texto do item e de uma linha em branco:

```
**** *dim_1_hipervigilancia *item_01
Sinto que preciso prestar atenção dobrada no meu modo de falar ou vestir para evitar ser mal interpretado(a) ou discriminado(a) no campus.
```

No corpus combinado entra uma variável a mais, que identifica a versão. Ela permite comparar versões e dimensões nas mesmas análises:

```
**** *v1 *dim_1_hipervigilancia *item_01
Sinto que preciso prestar atenção dobrada no meu modo de falar ou vestir para evitar ser mal interpretado(a) ou discriminado(a) no campus.
```

## Versões do instrumento

| Versão | Itens | Dimensões |
|---|---|---|
| v1 | 41 | 4 |
| v2 | 44 | 5 |
| v3 | 40 | 4 |
| v4 | 40 | 4 |
| v5 | 40 | 4 |

## Como gerar os corpus

Requer apenas Python 3, sem dependências externas.

```bash
python3 build_corpus.py
```

O script grava `corpus_v1.txt` a `corpus_v5.txt` e `corpus_combinado.txt` na pasta atual, em UTF-8. Para alterar algum item, edite o texto no dicionário `VERSOES` dentro do script e rode de novo.

## Como rodar a análise no IRAMUTEQ

Importe um dos arquivos `.txt` como corpus textual e siga estas etapas:

1. **Corpus textual**: carregar o arquivo no formato acima.
2. **Classificação Hierárquica Descendente (método Reinert)**: identifica classes de vocabulário e mostra se elas se alinham às dimensões.
3. **Análise de similitude**: mapeia a estrutura interna das relações entre as palavras.
4. **Análise Fatorial de Correspondência (AFC)**: plota as dimensões (e, no corpus combinado, as versões) no plano fatorial.

## Decisões de preparação do texto

- **Numeração dos itens**: renumerei de `item_01` em diante dentro de cada versão. A versão 1 tinha numeração repetida e pulada.
- **Anotações removidas**: tirei marcações de revisão como "(só para estudantes)", "(Funcionários)", "(Novo)" e comentários internos, para que não entrem como vocabulário na análise lexical.
- **Rótulos da dimensão 5 (v2)**: removi os títulos que antecediam cada item, como "Sustentabilidade do ritmo diário:", pelo mesmo motivo.
- **Correções mínimas**: corrigi um erro de digitação na v1 ("aos a outros colaboradores" virou "aos outros colaboradores") e padronizei a pontuação final dos itens.

## Pendências conhecidas

- O **item 16 da v4** está truncado no texto original ("...acessibilidade adequada no") e foi mantido assim. Precisa ser completado antes da análise.
- Na v5, a marcação de quais itens valem só para estudantes ou só para funcionários foi removida do texto. Se eu quiser comparar os dois públicos, posso acrescentar uma variável como `*publico_est` e `*publico_func` no cabeçalho.
