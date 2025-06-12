## Sistemas de Banco de Dados

Fundamentos em Bancos de Dados Relacionais



Material distribuído sob licença CC BY-NC-ND 4.0

Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International

## indexação multinível

## Indexação

 CC BY-NC-ND 4.0 quesecontróiíndices Índice multinível ! diferentes níveis de índices são construídos, reduzindo o espaço de pesquisa I Estático ! compacto, sem espaço extra em blocos de índice para acomodação de novos registros I Tipicamente implementado como arquivo de índice, em sobre índices I Dinâmico ! flexível, com espaço para alocação dinâmica de registros, tornando operações de alteração de dados mais eficientes I Tipicamente implementado como árvore B ( B Tree ) ou B+ ( B+ Tree ), estruturas baseadas em árvores de pesquisa de múltiplos caminhos, com restrições



## Índice Multinível Estático

 Nível Base ! índice com valores distintos no campo de ordenação Nível Subsequente ! índice primário sobre nível adjacente anterior PROFESSOR





## Índice Multinível Estático

## Derivam-se níves até que o n -ésimo nível seja armazenado em apenas um bloco







## Índice Multinível Estático

 CC BY-NC-ND 4.0 onívelbase Pesquisa ! complexidade logarítmica com base &gt; 2, apenas um bloco em cada nível precisa ser acessado I Base logarítmica ! fator de bloco do índice, ou fan-out ( fo ) I Níveis ! h GLYPH&lt;25&gt; d log fo r 1 e , onde r 1 é o número de registros n I Acessos a blocos ! A = h Alteração ! níveis ordenados, custo alto de operações de alteração do campo de indexação Arquivo ISAM (Indexed Sequential Access Method) ! arquivo sequencial indexado com índice multinível na chave primária



## Índice Multinível Estático

 discocombloCC BY-NC-ND 4.0 Para um arquivo indexado de Professor , com 200.000 registros de tamanho fixo de 185B, ordenado pela chave primária CPF e armazenado em um cos de 4KB, teremos: I Fator de Bloco ! F = j 4 KB 185 B k = j 4 GLYPH&lt;2&gt; 1 024 : B 185 B k GLYPH&lt;25&gt; b 22 14 ; c = 22 I # Blocos ! B = l 200 000 : 22 m GLYPH&lt;25&gt; d 9 090 91 : ; e = 9 091 : I Espaço ! S = 9 091 : GLYPH&lt;2&gt; 4 KB = 36 364 : KB GLYPH&lt;25&gt; 35 51 ; MB Pesquisas nesse arquivo demandarão acessos a blocos de disco: I Pela chave primária ! A = log d 2 9 091 : e GLYPH&lt;25&gt; d 13 15 ; e = 14 I Por outro campo ! A = 9 091 :



## Índice Multinível Estático

 CC BY-NC-ND 4.0040 Para Professor sendo arquivo ISAM, com CPF de 11B, e ponteiro de bloco ocupando 16B, teremos: I Fator de Bloco ! FM = j 4 KB 11 B + 16 B k = j 4 GLYPH&lt;2&gt; 1 024 : B 27 B k GLYPH&lt;25&gt; b 151 70 ; c = 151 I # Blocos ! BM 1 = l 9 091 : 151 m GLYPH&lt;25&gt; d 60 20 ; e = 61, BM 2 = l 61 151 m GLYPH&lt;25&gt; d ; e = 1 I Espaço ! SM =( 61 + ) 1 GLYPH&lt;2&gt; 4 KB = 248 KB Pesquisas nesse arquivo só podem ser realizadas pelo campo de indexação e demandarão acessos a blocos de disco: I AM = h GLYPH&lt;25&gt; d log 151 9 091 : e GLYPH&lt;25&gt; d 1 81 ; e = 2

- I + 1 acesso para recuperar o registro no arquivo indexado



## Índice Multinível Dinâmico

 Árvore ( Tree ) ! estrutura hierárquica de nós (elementos) conectados I Raiz ! nó sem pai, de nível zero I Folha ! nó sem filhos I Interno ! nó não folha e não raiz I Onível de um nó na árvore é o nível do seu pai mais um I Subárvore ! árvore formada por um nó e todos os seus descendentes

CC BY-NC-ND 4.0







## Índice Multinível Dinâmico

CC BY-NC-ND 4.0 oresdadireita

 Árvore de Busca ( Search Tree ) ! nós com restrições para eficiência em busca I Binária ! nó tem no máximo dois filhos I Chave não pode ser menor que qualquer outra em subárvores da esquerda I Chave não pode ser maior que qualquer outra em subárv





## Índice Multinível Dinâmico

 Árvore de busca binária (BST) ! balanceamento fundamental para eficiência I Balanceamento ! altura de árvore GLYPH&lt;25&gt; d log 2 n e , onde n = número de nós I Subárvores esquerda e direita com GLYPH&lt;25&gt; mesmo número de nós





## Índice Multinível Dinâmico



CC BY-NC-ND 4.0

 Árvore de busca de múltiplos caminhos ( m-way ) ! generalização de BST I Cada nó tem m filhos I Multiplicidade ! cada nó contém m GLYPH&lt;0&gt; 1 elementos I h GLYPH&lt;20&gt; n GLYPH&lt;20&gt; m h GLYPH&lt;0&gt; 1, onde h = altura e n = número de nós I Balanceamento ! h GLYPH&lt;25&gt; d log m n e



## Índice Multinível Dinâmico

- B Tree ! m-way com restrições que tornam busca e atualização muito eficientes
- I Nó raiz, não folha, tem ao menos dois filhos
- I Nó interno tem ao menos d m = 2 e filhos
- I Nós folha estão no mesmo nível







## Índice Multinível Dinâmico

CC BY-NC-ND 4.0

 B Tree ! nós ao menos meio cheios, GLYPH&lt;25&gt; 69 % quando árvore estabiliza I Pesquisa ! eficiente, poucos níveis e perfeitamente balanceada I Alteração ! eficiente, espaço para acomodar novos registros I Ideal para armazenamento em memória secundária I Tipicamente configurada para que um nó ocupe um bloco em disco I Elemento ! campo de indexação + ponteiro de bloco ( 4 ) I Nó com m ponteiros de nó ( GLYPH&lt;15&gt; ), um para cada filho





## Índice Multinível Dinâmico

CC BY-NC-ND 4.0

 locode16B Arquivo de Professor , com índice B Tree em Departamento de 8B, com um nó ocupando um bloco de disco, ponteiro de nó de 12B, ponteiro de b I Tamanho do elemento ! ( 8 B + 16 B ) = 24 B I Nó ocupa 1 bloco ! 4 KB GLYPH&lt;21&gt; (( m GLYPH&lt;0&gt; 1 ) GLYPH&lt;2&gt; ( 24 B + 12 B )) + 12 B I # Elementos por nó ! ( m GLYPH&lt;0&gt; 1 ) = j 4 KB GLYPH&lt;0&gt; 12 B 24 B + 12 B k = j 4 084 : B 36 B k GLYPH&lt;25&gt; b 113 44 ; c = 113 I Ordem da árvore ! m = 113 + 1 = 114 I Altura da árvore ! h GLYPH&lt;25&gt; d log 114 200 000 : e GLYPH&lt;25&gt; d 2 57 ; e = 3

|   Nível | # Nós   | # Registros   | # Ponteiros de Nó   |
|---------|---------|---------------|---------------------|
|       0 | 1       | 113           | 114                 |
|       1 | CC 114  | 12.882        | 12.996              |
|       2 | 12.996  | 1.468.584     | -                   |



## Índice Multinível Dinâmico

 CC BY-NC-ND 4.0 Considerando uma ocupação de nós em 69%: I Fator de Bloco ! FB = d 113 GLYPH&lt;2&gt; 0 69 : e GLYPH&lt;25&gt; d 77 97 ; e = 78 I # Blocos ! BB = l 200 000 : 78 m GLYPH&lt;25&gt; d 2 564 10 : ; e = 2 565 : I Espaço ! SB = 2 565 : GLYPH&lt;2&gt; 4 KB = 10 260 : KB GLYPH&lt;25&gt; 10 01 ; MB Pesquisas nesse índice só podem ser realizadas pelo campo de indexação e demandarão acessos a blocos de disco: I AB = h = 3 I + 1 acesso para recuperar o registro no arquivo indexado 



## Índice Multinível Dinâmico

 B+ Tree ! extensão B Tree com restrições que tornam ainda mais eficientes a busca e a remoção I Nó Índice ! raiz ou interno que armazena exclusivamente chave I Nó Registro ! folha que armazena registro de índice I Nós folha em lista encadeada ordenada



CC BY-NC-ND 4.0





## Índice Multinível Dinâmico

CC BY-NC-ND 4.0

 locode16B Arquivo de Professor , com índice B+ Tree em Departamento de 8B, com um nó ocupando um bloco de disco, ponteiro de nó de 12B, ponteiro de b I Nó Índice I Tamanho do elemento ! 8 B I Nó ocupa 1 bloco ! 4 KB GLYPH&lt;21&gt; (( m GLYPH&lt;0&gt; 1 ) GLYPH&lt;2&gt; ( 8 B + 12 B )) + 12 B I Elementos por nó ! ( m GLYPH&lt;0&gt; 1 ) = j 4 KB GLYPH&lt;0&gt; 12 B 8 B + 12 B k = j 4 084 : B 20 B k GLYPH&lt;25&gt; b 204 2 ; c = 204 I Ordem da árvore ! m = 204 + 1 = 205 I Altura da árvore ! h GLYPH&lt;25&gt; d log 205 200 000 : e GLYPH&lt;25&gt; d 2 29 ; e = 3 I Altura de nós índice ! hi = h GLYPH&lt;0&gt; 1 = 2



## Índice Multinível Dinâmico

|   Nível |   # Nós | # Registros   | # Ponteiros de Nó   |
|---------|---------|---------------|---------------------|
|       0 |   1     | 204           | 205                 |
|       1 | 205     | 41.820        | 42.025              |
|       2 |  42.025 | 8.573.100     | -                   |

## I Nó Registro

CC BY-NC-ND 4.0

 I Tamanho do elemento ! ( 8 B + 16 B ) = 24 B I Nó ocupa 1 bloco ! 4 KB GLYPH&lt;21&gt; (( m GLYPH&lt;0&gt; 1 ) GLYPH&lt;2&gt; ( 24 B )) + 12 B I Elementos por nó ! ( m GLYPH&lt;0&gt; 1 ) = j 4 KB GLYPH&lt;0&gt; 12 B 24 B k = j 4 084 : B 24 B k GLYPH&lt;25&gt; b 170 16 ; c = 170



## Índice Multinível Dinâmico

 CC BY-NC-ND 4.0 Considerando uma ocupação de nós em 69%: I Fator de Bloco ! FB + = d 170 GLYPH&lt;2&gt; 0 69 : e GLYPH&lt;25&gt; d 117 30 ; e = 118 I # Blocos ! BB + = l 200 000 : 118 m GLYPH&lt;25&gt; d 1 694 91 : ; e = 1 695 : I Nível 0 a hi GLYPH&lt;0&gt; 1 ! 1 695 ponteiros : I # Nós = # Blocos = ! d GLYPH&lt;24&gt; 1 695 : ( 204 GLYPH&lt;2&gt; 0 69 : ) e + hi GLYPH&lt;25&gt; GLYPH&lt;25&gt; l 1 695 : 143 m GLYPH&lt;25&gt; d 11 85 ; e = 12 I Espaço ! SB + =( 1 695 : + 12 ) GLYPH&lt;2&gt; 4 KB = 6 828 : KB GLYPH&lt;25&gt; 6 67 ; MB Pesquisas pelo campo de indexação demandam acessos a blocos: I AB + = h = 3 I + 1 acesso para recuperar o registro no arquivo indexado



## Referências Bibliográficas

- [1] Elmasri, Ramez; Navathe, Sham. Fundamentals of Database Systems . 7ed. Pearson, 2016.
- [2] Silberschatz, Abraham; Korth, Henry F.; Sudarshan, S. Database System Concepts . 6ed. McGraw-Hill, 2011.
- [3] Date, Christopher J. An Introduction to Database Systems . 8ed. Pearson, 2004.



## Sistemas de Banco de Dados

Fundamentos em Bancos de Dados Relacionais



Material distribuído sob licença CC BY-NC-ND 4.0

Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International

## indexação de nível único



## Indexação

Construção de índices para acelerar recuperação de registros de arquivos Índice ! Caminho alternativo de acesso a registros de um arquivo

ÍNDICE

CC BY-NC-ND 4.0 #00



| CPF                        | Nome                       | Sexo                       | Salario                    | Cardoso Departamento       | 4.0 #00   | Ponteiro                   | Departamento               |
|----------------------------|----------------------------|----------------------------|----------------------------|----------------------------|-----------|----------------------------|----------------------------|
| 12345678900                | Roberto Machado            | M                          | 1200.00                    | 1                          | 4.0 #00   | #00                        | 1                          |
| 21345678900                | Carlos A. Martins          | M                          | 3200.00                    | 1                          | 4.0 #00   | #10                        | 2                          |
| 32145678900                | Ana Maria Freitas          | F                          | 7500.00                    | 2                          | #10       | GLYPH<1> GLYPH<1> GLYPH<1> | GLYPH<1> GLYPH<1> GLYPH<1> |
| GLYPH<1> GLYPH<1> GLYPH<1> | GLYPH<1> GLYPH<1> GLYPH<1> | GLYPH<1> GLYPH<1> GLYPH<1> | GLYPH<1> GLYPH<1> GLYPH<1> | GLYPH<1> GLYPH<1> GLYPH<1> | 4.0 #00   | #FF                        | N                          |
| 52345678902                | Luiz A. Barbosa            | M                          | 5300.00                    | N                          | #FF       |                            |                            |

- I Registro ! campos de indexação + ponteiro para bloco que armazena o registro do arquivo indexado referenciado pelos campos de indexação

 PROFESSOR I Arquivo de índice ! arquivo adicional ao arquivo de dados (indexado) I Contém campos de indexação provenientes do arquivo indexado



## Indexação

|         CPF | Nome              | Sexo   |   Salario |   Departamento |         | Ponteiro   |   Departamento |
|-------------|-------------------|--------|-----------|----------------|---------|------------|----------------|
| 12345678900 | Roberto Machado   | M      |      1200 |              1 | 4.0 #00 | #00        |              1 |
| 21345678900 | Carlos A. Martins | M      |      3200 |              1 | 4.0 #00 | #00        |              1 |
| 32145678900 | Ana Maria Freitas | F      |      7500 |              2 | #10     | #10        |              2 |

ÍNDICE

|             |                    | Sexo   | Salario   | Departamento   |     |          |              |
|-------------|--------------------|--------|-----------|----------------|-----|----------|--------------|
| CPF         | Nome               |        |           |                |     | Ponteiro | Departamento |
| 12345678900 | CC Roberto Machado | M      | 1200.00   | 1              | #00 | #00      | 1            |
| 21345678900 | Carlos A. Martins  | M      | 3200.00   | 1              | #00 | #10      | 2            |
| 32145678900 | Ana Maria Freitas  | F      | 7500.00   | 2              | #10 |          |              |

CC BY-NC-ND 4.0

 Índice de nível único ! arquivo ordenado pelo campo de indexação I Denso ! um registro de índice para cada registro no arquivo indexado PROFESSOR ÍNDICE I Esparso ! registros de índice para alguns registros no arquivo indexado PROFESSOR



## Índice Primário

ÍNDICE

CC BY-NC-ND 4.0 0 #1

 Índice esparso com registros de tamanho fixo PROFESSOR I Campo de indexação ! referencia chave primária do arquivo indexado I Demanda arquivo indexado ordenado pela chave primária I Umregistro de índice para cada bloco do arquivo indexado

|         CPF | Nome              | Sexo   | Salario         |   Departamento | #00   | Ponteiro   | CPF         |
|-------------|-------------------|--------|-----------------|----------------|-------|------------|-------------|
| 12345678900 | Roberto Machado   | M      | 1200.00         |              1 | #00   | #00        | 12345678900 |
| 12345678901 | Manuela Costa     | F      | 2700.00         |              3 | #00   | #10        | 21345678900 |
| 21345678900 | Carlos A. Martins | M      | 3200.00         |              1 | #00   | #20        | 52345678902 |
| 32145678900 | Ana Maria Freitas | F      | Cardoso 7500.00 |              2 | #10   | 4.0        |             |
| 52345678902 | Luiz A. Barbosa   | M      | 5300.00         |              3 | #20   |            |             |

- I Primeiro registro de cada bloco do arquivo indexado (âncora do bloco) encontra-se referenciado por um registro no arquivo de índice



## Índice Primário

 discocom CC BY-NC-ND 4.0 Para um arquivo indexado de Professor , com 10.000 registros de tamanho fixo de 185B, ordenado pela chave primária CPF e armazenado em um blocos de 4KB, teremos: I Fator de Bloco ! F = j 4 KB 185 B k = j 4 GLYPH&lt;2&gt; 1 024 : B 185 B k GLYPH&lt;25&gt; b 22 14 ; c = 22 I # Blocos ! B = l 10 000 : 22 m GLYPH&lt;25&gt; d 454 54 ; e = 455 I Espaço ! S = 455 GLYPH&lt;2&gt; 4 KB = 1 820 : KB GLYPH&lt;25&gt; 1 77 ; MB Pesquisas nesse arquivo demandarão acessos a blocos de disco: I Pela chave primária ! A = d log 2 455 e GLYPH&lt;25&gt; d 8 83 ; e = 9

- I Por outro campo ! A = 455



## Índice Primário

 CC BY-NC-ND 4.0 Para um índice primário criado sobre a chave primária CPF de 11B, onde o ponteiro de bloco ocupa 16B, teremos: I Fator de Bloco ! FP = j 4 KB 11 B + 16 B k = j 4 GLYPH&lt;2&gt; 1 024 : B 27 B k GLYPH&lt;25&gt; b 151 70 ; c = 151 I # Blocos ! BP = l 455 151 m GLYPH&lt;25&gt; d 3 01 ; e = 4 I Espaço ! SP = 4 GLYPH&lt;2&gt; 4 KB = 16 KB Pesquisas nesse arquivo só podem ser realizadas pelo campo de indexação e demandarão acessos a blocos de disco: I AP = d log 2 4 e = 2

- I + 1 acesso para recuperar o registro no arquivo indexado



## Índice Primário

 CC BY-NC-ND 4.0 oarquivoindexado Arquivo de índice é significativamente menor que arquivo indexado, ocupando menos blocos em disco I Esparsidade ! menos registros no arquivo de índice I Tamanho ! registros de índice menores que registros d I Ordenação ! arquivo ordenado com pesquisa de complexidade logarítmica I Pesquisa binária no arquivo de índice para encontrar a chave procurada I Acesso direto ao registro de dados através do endereço de bloco recuperado a partir do índice Operações de atualização no arquivo indexado podem envolver reordenação de registros do próprio arquivo indexado e do arquivo de índice



## Índice de Agrupamento

## Ou índice clustering , é um índice esparso com registros de tamanho fixo

## PROFESSOR

ÍNDICE

- CC BY-NC-ND 4.0 #10 32145678900 12345678901 52345678902 I Campo de indexação ! referencia campo de agrupamento (chave não exclusiva) do arquivo indexado I Demanda arquivo indexado ordenado pelo campo de agrupamento I Umregistro de índice para cada valor distinto no campo de agrupamento



|         CPF | Nome              | Sexo   | Salario         |   Departamento |     | Ponteiro   | Departamento   |
|-------------|-------------------|--------|-----------------|----------------|-----|------------|----------------|
| 12345678900 | Roberto Machado   | M      | 1200.00         |              1 | #10 | #00        | 1              |
| 21345678900 | Carlos A. Martins | M      | 3200.00         |              1 | #10 | #10        | 2              |
| 32145678900 | Ana Maria Freitas | F      | 7500.00         |              2 |     | #10        | 3              |
| 12345678901 | Manuela Costa     | F      | Cardoso 2700.00 |              3 | #00 | 4.0        |                |
| 52345678902 | Luiz A. Barbosa   | M      | 5300.00         |              3 | #20 |            |                |

- I Bloco de primeira ocorrência de um valor distinto no campo de agrupamento encontra-se referenciado por um registro no arquivo de índice



## Índice de Agrupamento

 eoponteirode CC BY-NC-ND 4.0 No arquivo indexado de Professor , para um índice de agrupamento criado sobre o campo Departamento de 8B, contendo 200 valores distintos, ond bloco ocupa 16B, teremos: I Fator de Bloco ! FC = j 4 KB 8 B + 16 B k = j 4 GLYPH&lt;2&gt; 1 024 : B 24 B k GLYPH&lt;25&gt; b 170 66 ; c = 170 I # Blocos ! BC = l 200 170 m GLYPH&lt;25&gt; d 1 17 ; e = 2 I Espaço ! SC = 2 GLYPH&lt;2&gt; 4 KB = 8 KB Pesquisas nesse arquivo só podem ser realizadas pelo campo de indexação e demandarão acessos a blocos de disco:

- I AC = d log 2 2 e = 1
- I + 1 acesso para recuperar o registro no arquivo indexado



## Índice Secundário

ÍNDICE

CC BY-NC-ND 4.0 0 #1

 Índice denso com registros de tamanho fixo PROFESSOR I Campo de indexação ! referencia campo não ordenado do arquivo indexado I Não demanda ordenação no arquivo indexado I Umregistro de índice para cada registro do arquivo indexado

|         CPF | Nome              | Sexo   | Salario         |   Departamento | 4.0 #00   | Ponteiro   |   Departamento |
|-------------|-------------------|--------|-----------------|----------------|-----------|------------|----------------|
| 12345678900 | Roberto Machado   | M      | 1200.00         |              1 | 4.0 #00   | #00        |              1 |
| 12345678901 | Manuela Costa     | F      | 2700.00         |              3 | 4.0 #00   | #10        |              1 |
| 21345678900 | Carlos A. Martins | M      | 3200.00         |              1 | 4.0 #00   | #10        |              2 |
| 32145678900 | Ana Maria Freitas | F      | Cardoso 7500.00 |              2 | #10       | #00        |              3 |
| 52345678902 | Luiz A. Barbosa   | M      | 5300.00         |              3 | #20       | #20        |              3 |

- I Bloco de cada registro do arquivo indexado encontra-se referenciado por um registro no arquivo de índice



## Índice Secundário

 teremos: CC BY-NC-ND 4.0 No arquivo indexado de Professor , para um índice secundário criado sobre o campo Departamento de 8B, onde o ponteiro de bloco ocupa 16B, I Fator de Bloco ! FS = j 4 KB 8 B + 16 B k = j 4 GLYPH&lt;2&gt; 1 024 : B 24 B k GLYPH&lt;25&gt; b 170 66 ; c = 170 I # Blocos ! BS = l 10 000 : 170 m GLYPH&lt;25&gt; d 58 82 ; e = 59 I Espaço ! SS = 59 GLYPH&lt;2&gt; 4 KB = 236 KB Pesquisas nesse arquivo só podem ser realizadas pelo campo de indexação e demandarão acessos a blocos de disco: I AS = d log 2 59 e GLYPH&lt;25&gt; d 5 88 ; e = 6

- I + 1 acesso para recuperar o registro no arquivo indexado



## Índice Secundário

 CC BY-NC-ND 4.0 ivo Arquivo de índice tipicamente menor que arquivo indexado I Tamanho ! registros de índice menores que registros do arquivo indexado I Ordenação ! arquivo ordenado com pesquisa binária I Flexibilidade ! múltiplos índices sobre um mesmo arqu I Não demandam arquivo indexado ordenado I Somente um índice primário ou de agrupamento por arquivo indexado, por demandarem ordenação I Desempenho ! proporcionalmente, maior ganho em tempo de pesquisa I Para índices primário ou de agrupamento, tem-se a opção de pesquisa binária tanto no arquivo indexado, quanto no arquivo índice



## Indexação

| Tipo        | Esparsidade   | Arquivo Indexado   | Quantidade Registros                                    |
|-------------|---------------|--------------------|---------------------------------------------------------|
| Primário    | Esparso       | Cardoso Ordenado   | Número de blocos do arquivo in- dexado                  |
| Agrupamento | Esparso       | Ordenado           | 4.0 Número de valores distintos no campo de agrupamento |
| Secundário  | Denso         | Qualquer           | Número de registros do arquivo indexado                 |

 Comparativo entre diferentes tipos de índices de nível único

CC BY-NC-ND 4.0





## Referências Bibliográficas

- [1] Elmasri, Ramez; Navathe, Sham. Fundamentals of Database Systems . 7ed. Pearson, 2016.
- [2] Silberschatz, Abraham; Korth, Henry F.; Sudarshan, S. Database System Concepts . 6ed. McGraw-Hill, 2011.
- [3] Date, Christopher J. An Introduction to Database Systems . 8ed. Pearson, 2004.



## Sistemas de Banco de Dados

Fundamentos em Bancos de Dados Relacionais



Material distribuído sob licença CC BY-NC-ND 4.0

Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International

## modelo entidade-relacionamento



## Modelo Entidade-Relacionamento (ER)

Modelo conceitual elaborado a partir da especificação do minimundo

- I Minimundo ! tipicamente especificado de forma textual, estabelecendo os requisitos de dados
- CC BY-NC-ND 4.0 ráficadeentidades, I Diagrama Entidade-Relacionamento ! representação g atributos, relacionamentos e restrições do modelo ER Cliente Nome Rua Cidade Possui Conta Número Saldo 1 N







## ER: Entidade

## Ente com existência real no minimundo especificado

- I Seja E = f e 1 ; e 2 ; GLYPH&lt;1&gt; GLYPH&lt;1&gt; GLYPH&lt;1&gt; ; ek g um conjunto de k entidades de mesmo tipo
- I Tipo de Entidade ( E ) ! conjunto de instâncias de entidades do mesmo tipo
- CC BY-NC-ND 4.0 deentidade I Instância de Entidade ( ei ) ! ente específico de um tipo E , tal que ei 2 E e 1 e 2 E









## ER: Entidade

No diagrama ER representa-se um tipo de entidade, ou simplesmente entidade, como um retângulo rotulado







## ER: Entidade

Entidade Fraca ! entidade que existência depende da existência de outra



CC BY-NC-ND 4.0





## ER: Atributo

Propriedade que descreve uma característica específica de uma entidade

Representa-se como uma elipse rotulada e ligada à entidade que ele caracteriza







## ER: Atributo

Simples ! indivisível, representado por uma elipse simples rotulada







## ER: Atributo

Composto ! desmembra-se em outros atributos, representado por uma elipse simples rotulada com outros atributos ligados a ele







## ER: Atributo

Multivalorado ! conteúdo formado por mais de um valor, representado por uma elipse rotulada com borda dupla







## ER: Atributo

 Derivado ! valor obtido a partir de valores de outros atributos ou relacionamentos, representado por uma elipse rotulada com bord



 atracejada



## ER: Atributo

 mplesrotulada CC BY-NC-ND 4.0 Chave ! atributo ou conjunto de atributos que juntos identificam cada instância de entidade de maneira exclusiva, representado por uma elipse si com rótulo sublinhado Funcionário CPF Nome Primeiro Sobrenome Sexo Salário Data Nascimento





## ER: Atributo



 aneira CC BY-NC-ND 4.0 Chave Parcial ! ou discriminador , atributo ou conjunto de atributos que juntos potencialmente identificam cada instância de entidade fraca de m exclusiva, representado por uma elipse simples rotulada com rótulo sublinhado de maneira tracejada Nome



## ER: Relacionamento

## Associação entre entidades

- I Seja R = f r 1 ; r 2 ; GLYPH&lt;1&gt; GLYPH&lt;1&gt; GLYPH&lt;1&gt; ; r k g um conjunto de k associações entre entidades
- I Tipo de Relacionamento ( R ) ! conjunto de instâncias de associações do mesmo tipo
- CC BY-NC-ND 4.0 I Instância de Relacionamento ( r i ) ! associação específica entre instâncias de entidades, tal que r i 2 R e 1 e 2 e 3 E r 1 r 2 r 3 R e 1 e 2 e 3 E







## ER: Relacionamento

No diagrama ER representa-se um tipo de relacionamento, ou simplesmente relacionamento, como um losango rotulado







## ER: Relacionamento

Relacionamento Fraco ! ou de dependência , associação envolvendo ao menos uma entidade fraca, representado por um losango rotulado com b



CC BY-NC-ND 4.0

 ordadupla



## ER: Relacionamento

Cada relacionamento r i 2 R é uma associação entre entidades que inclui exatamente uma única instância de cada entidade participante



Grau do Relacionamento ! # entidades participantes no relacionamento

- I Binário ! grau 2



- I Ternário ! grau 3

CC BY-NC-ND 4.0





## ER: Relacionamento

Nome de Função ! rotula o relacionamento e representa a função que uma entidade desempenha em cada relacionamento

- I Enriquece a semântica do relacionamento





No relacionamento possui , Funcionário desempenha a função possuído , enquanto Departamento desempenha a função possuidor

CC BY-NC-ND 4.0





## ER: Relacionamento

Relacionamento Recursivo ! a mesma entidade participa mais de uma vez, com funções diferentes, em um relacionamento



CC BY-NC-ND 4.0 Funcionário Nome Sexo supervisiona No exemplo, Funcionário participa com as funções de supervisor e supervisionado no relacionamento supervisiona





## ER: Restrição

Característica limitadora da possibilidade de associação entre entidades nos relacionamentos

- I Razão de Participação ! especifica se a participação de uma entidade no relacionamento é parcial ou total
- CC BY-NC-ND 4.0 I Razão de Cardinalidade ! especifica o número máximo de relacionamentos em que uma entidade pode participar, opcionalmente indica limites mínimos Funcionário CPF Nome Sexo possui Departamento Nome Locais N 1 (0, N) (1, 1)







## ER: Restrição

Participação Total ! todas as instâncias da entidade devem obrigatoriamente participar de relacionamentos



Representa-se por uma linha dupla entre a entidade e o relacionamento





CC BY-NC-ND 4.0





## ER: Restrição

## Cardinalidade 1:1 ! uma instância de cada entidade só pode participar de um único relacionamento



Representa-se por rótulos 1 nas duas extremidades do relacionamento



CC BY-NC-ND 4.0





## ER: Restrição



 Cardinalidade 1:N ! uma instância de uma entidade só pode participar de um relacionamento, enquanto uma instância da outra pode participa Representa-se por rótulos 1 em uma extremidade e N na outra



CC BY-NC-ND 4.0

 rdemúltiplos



## ER: Restrição

Cardinalidade N:N ! uma instância de qualquer entidade pode participar de múltiplos relacionamentos



Representa-se por rótulos N nas duas extremidades do relacionamento





CC BY-NC-ND 4.0





## ER: Restrição

Mínimos e Máximos ! opcionalmente pode-se definir limites mínimos e máximos de cardinalidade para os relacionamentos

Representa-se por rótulos (min, max) nas duas extremidades do relacionamento







## ER: Convenção de Nomes

CC BY-NC-ND 4.0

 Elementos do modelo ER referenciam elementos textuais em uma especificação textual de minimundo I Substantivo ! pode indicar entidade ou atributo I Verbo ! pode indicar relacionamento Para a construção do diagrama ER deve-se adotar uma convenção, por exemplo: I Entidade ! nome no singular com letra inicial em maiúscula I Relacionamento ! nome no singular com todas as letras minúsculas I Atributo ! nome com as letras iniciais em maiúscula e atributo multivalorado com nome no plural



## ER: Resumo de Elementos





## ER: Resumo de Elementos





## Referências Bibliográficas

- [1] Elmasri, Ramez; Navathe, Sham. Fundamentals of Database Systems . 7ed. Pearson, 2016.
- [2] Silberschatz, Abraham; Korth, Henry F.; Sudarshan, S. Database System Concepts . 6ed. McGraw-Hill, 2011.
- [3] Date, Christopher J. An Introduction to Database Systems . 8ed. Pearson, 2004.



## Sistemas de Banco de Dados

Fundamentos em Bancos de Dados Relacionais



Material distribuído sob licença CC BY-NC-ND 4.0

Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International

## esquema e linguagem



## Esquema de BD

- I Construtor de Esquema ! elemento que compõe o esquema, como por exemplo professor

 CC BY-NC-ND 4.0 Descrição do banco de dados (metadados) I Especificado no projeto e não muda com frequência I Existem convenções para se representar esquemas usando diagramas I Diagrama de Esquema ! representação de um esquema I Capta aspectos como restrições, tipos de registros e de itens de dados PROFESSOR CPF Nome Sexo Salario Departamento



## Esquema de BD

Odiagrama de esquema apresenta a estrutura de cada tipo de elemento, mas NÃO apresenta as instâncias dos elementos

|         CPF | Nome              | Sexo   | Salario     |   Departamento |
|-------------|-------------------|--------|-------------|----------------|
| 12345678900 | Roberto Machado   | M      | 4.0 1200.00 |              1 |
| 12345678901 | Manuela Costa     | F      | 2700.00     |              3 |
| 21345678900 | Carlos A. Martins | M      | 3200.00     |              1 |
| 32145678900 | Ana Maria Freitas | F      | 7500.00     |              2 |

CC BY-NC-ND 4.0

 PROFESSOR





## Instância de BD

CC BY-NC-ND 4.0 valordeumitem

 Conjunto de dados armazenados em determinado momento I Estado Vazio ! esquema especificado, mas nenhum dado armazenado I Estado Inicial ! BD carregado (populado) com dados inicias I Estado se altera ao se inserir , remover ou modificar o



## Arquitetura de Três Esquemas

-  CC BY-NC-ND 4.0 macessorestritoa Abordagem que permite visualização do esquema em diferentes níveis I Autodescrição ! metadados descritivos em diferentes níveis de abstração, de acordo com características estruturais I Suporte a Múltiplas Visões ! usuários e aplicações tê porções do BD suficientes para atender suas necessidades I Independência de Aplicação ! estrutura do BD armazenada separadamente de aplicações, garantindo que alterações na estrutura não necessariamente levem a mudanças em aplicações



## Arquitetura de Três Esquemas







## Arquitetura de Três Esquemas

## I Nível Externo

## I Nível Conceitual

- I Nível Interno

 CC BY-NC-ND 4.0 I Esquema Externo ! visões de usuário I Cada visão descreve a parte do BD em que um grupo de usuários está interessado, ocultando o restante I Implementado com modelo de dados representativo I Esquema Conceitual ! estrutura do BD I Descrição de tipos de dados, entidades, relacionamentos, restrições e operações do usuário I Oculta detalhes de armazenamento físico I Esquema Físico ! estrutura do armazenamento físico do BD

- I Descrição de detalhes de armazenamento de dados e de caminhos de acesso



## Arquitetura de Três Esquemas

-  CC BY-NC-ND 4.0 áriosemuma Níveis apresentam descritores para dados que estão efetivamente armazenados em meio físico I Mapeamento ! transformação de requisições e resultados entre níveis I SGBD transforma uma solicitação especificada por usu solicitação no esquema conceitual e, em seguida, em uma solicitação no esquema interno para que o processamento de dados possa ser realizado



## Independência de Dados

 CC BY-NC-ND 4.0 Capacidade de se alterar o esquema em um nível sem precisar alterar o esquema no nível adjacente superior I Lógica ! capacidade de alterar o esquema conceitual sem precisar alterar o esquema externo I Exemplo ! ao acrescentar ou remover um tipo de dado somente o mapeamento entre os níveis e a definição da visão são alterados I Física ! capacidade de alterar o esquema interno sem precisar alterar o esquema conceitual I Exemplo ! ao organizar arquivos físicos criando estruturas de acesso adicionais somente o mapeamento entre os níveis é alterado



## Independência de Dados

-  CC BY-NC-ND 4.0 etrêsesquemas A arquitetura de três esquemas facilita a independência de dados I Independência lógica é mais difícil de ser alcançada, uma vez que é mais difícil realizar alterações estruturais e de restrição sem afetar as aplicações I Poucos SGBDs comerciais implementam a arquitetura d completamente por haver uma sobrecarga com os mapeamentos, levando a ineficiência



## Linguagens

Abordagem de BD precisa oferecer linguagens e interfaces apropriadas para cada tipo de usuário

- I VDL ! linguagem de definição de visão que especifica o esquema externo, as visões de usuário e seus mapeamentos ao esquema c
- CC BY-NC-ND 4.0 onceitual I DDL ! linguagem de definição de dados que especifica o esquema conceitual I SDL ! linguagem de definição de armazenamento que especifica o esquema interno I DML ! linguagem de manipulação de dados utilizada para especificação de operações de inserção, exclusão, modificação e recuperação de dados





## Linguagens

 CC BY-NC-ND 4.0 o Se diferenciam quanto à forma como as operações são especificadas I Alto Nível ! não procedural I Especifica operações complexas de forma concisa I Pode recuperar muitos registros em uma única instruçã I Declarativa ! especifica quais dados recuperar e não como I Denominada linguagem de consulta por ser usada de maneira interativa I Baixo Nível ! procedural I Embutida em linguagem de programação de uso geral (linguagem hospedeira), sendo assim denominada sublinguagem de dados I Recupera objetos ou registros individuais e os processa separadamente



## Linguagens

-  CC BY-NC-ND 4.0 SGBDs tipicamente não consideram as diferentes linguagens como distintas I SQL ! linguagem de consulta estruturada que combina VDL, DDL, SDL e DML, bem como instruções para especificação de restrição, evolução de esquema e outros recursos





## Referências Bibliográficas

- [1] Elmasri, Ramez; Navathe, Sham. Fundamentals of Database Systems . 7ed. Pearson, 2016.
- [2] Silberschatz, Abraham; Korth, Henry F.; Sudarshan, S. Database System Concepts . 6ed. McGraw-Hill, 2011.
- [3] Date, Christopher J. An Introduction to Database Systems . 8ed. Pearson, 2004.



## Sistemas de Banco de Dados

Fundamentos em Bancos de Dados Relacionais



Material distribuído sob licença CC BY-NC-ND 4.0

Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International

## álgebra relacional ii



## Operação PROJEÇÃO



 CC BY-NC-ND 4.0 Projeção Generalizada ! estende operação de projeção permitindo que funções sejam incluídas na lista de atributos para projeção Æ funcoes ( R ) Funções envolvem operações aritméticas e valores constantes Exemplo: A Æ CPF ; Nome + 0 0 + Sobrenome ; Salario GLYPH&lt;3&gt; 1 1 : ( PROFESSOR ) B GLYPH&lt;226&gt; CPF ; NomeCompleto ; Bonus ( A )



## Operação JUNÇÃO

|         CPF | Nome    | Sexo   |   Salario |   Departamento |
|-------------|---------|--------|-----------|----------------|
| 12345678900 | Roberto | M      |      1200 |              1 |
| 12345678901 | Manuela | F      |      2700 |              3 |

|   4.0 Numero | Nome           |
|--------------|----------------|
|            1 | Administrativo |
|            2 | Comercial      |
|            3 | Tecnologia     |

|         CPF | Nome       | Sexo   |   Salario |   Departamento |   Numero | Nome           |
|-------------|------------|--------|-----------|----------------|----------|----------------|
| 12345678900 | CC Roberto | M      |      1200 |              1 |        1 | Administrativo |
| 12345678901 | Manuela    | F      |      2700 |              3 |        3 | Tecnologia     |

CC BY-NC-ND 4.0

 Junção Interna (INNER JOIN) ! operação de junção convencional (JOIN) Exemplo ! PROFESSOR Z Departamento = Numero DEPARTAMENTO PROFESSOR DEPARTAMENTO Resultado:



## Operação JUNÇÃO

|         CPF | Nome    | Sexo   |   Salario |   Departamento |
|-------------|---------|--------|-----------|----------------|
| 12345678900 | Roberto | M      |      1200 |              1 |
| 12345678901 | Manuela | F      |      2700 |              3 |

|   Numero | Nome           |
|----------|----------------|
|        1 | Administrativo |
|        2 | Comercial      |
|        3 | Tecnologia     |

| CPF         | Nome    | Sexo   | Salario   | Departamento   |   Numero | Nome           |
|-------------|---------|--------|-----------|----------------|----------|----------------|
| 12345678900 | Roberto | M      | 1200.00   | 1              |        1 | Administrativo |
| 12345678901 | Manuela | F      | 2700.00   | 3              |        3 | Tecnologia     |
|             |         |        |           |                |        2 | Comercial      |

 CC BY-NC-ND 4.0 NTO Junção Externa (OUTER JOIN) ! a "relação externa" participa com tuplas não correspondentes da junção interna Exemplo ! PROFESSOR n Departamento = Numero DEPARTAMENTO PROFESSOR DEPARTAME Resultado:



## Operação JUNÇÃO

 CC BY-NC-ND 4.0 Junção Externa à Esquerda (LEFT OUTER JOIN) ! junção externa em que a "relação externa" é a da esquerda PROFESSOR o Departamento = Numero DEPARTAMENTO Junção Externa à Direita (RIGHT OUTER JOIN) ! junção externa em que a "relação externa" é a da direita PROFESSOR n Departamento = Numero DEPARTAMENTO Junção Externa Completa (FULL OUTER JOIN) ! junção externa em que ambas as relações são "externas"

PROFESSOR [ Departamento = Numero DEPARTAMENTO



## Operações de Conjunto

 CC BY-NC-ND 4.0 ões Operações da teoria dos conjuntos usadas para mesclar elementos de dois conjuntos , através de operações binárias I União ! adiciona todas as tuplas de ambas as relações I Interseção ! adiciona as tuplas comuns entre as relaç I Diferença ! adiciona as tuplas da primeira relação que não pertencem à segunda relação Relações devem ser compatíveis, possuindo o mesmo número de atributos alinhados de acordo com o domínio de dados Tuplas duplicadas são eliminadas da relação resultante

Nomes dos atributos da primeira relação são mantidos na relação resultante 



## Operações UNIÃO

- I Operador ! unir ( [ )
- I Função ! unir tuplas de duas relações
- I Operação comutativa

## Exemplo ! PROFESSOR [ ALUNO

## PROFESSOR

| Nome            |   Depto |
|-----------------|---------|
| Roberto Machado |       1 |
| Manuela Costa   |       3 |

| Nome            |   Departamento |
|-----------------|----------------|
| Roberto Machado |              2 |
| Manuela Costa   |              3 |

 CC BY-NC-ND 4.0 R 1 [ R 2 R 1 [ R 2 = R 2 [ R 1 ALUNO UNIÃO

| Nome            |   Depto |
|-----------------|---------|
| Roberto Machado |       1 |
| Manuela Costa   |       3 |
| Roberto Machado |       2 |



## Operações INTERSEÇÃO

 CC BY-NC-ND 4.0 R 1 \ R 2 I Operador ! intersecionar ( \ ) I Função ! selecionar tuplas comuns nas duas relações I Operação comutativa R 1 \ R 2 = R 2 \ R 1 Exemplo ! PROFESSOR \ ALUNO PROFESSOR ALUNO INTERSEÇÃO

| Nome            |   Depto |
|-----------------|---------|
| Roberto Machado |       1 |
| Manuela Costa   |       3 |

| Nome            |   Departamento |
|-----------------|----------------|
| Roberto Machado |              2 |
| Manuela Costa   |              3 |

| Nome          |   Depto |
|---------------|---------|
| Manuela Costa |       3 |



## Operações DIFERENÇA

 CC BY-NC-ND 4.0 ntidasnasegunda R 1 GLYPH&lt;0&gt; R 2 I Operador ! menos ( GLYPH&lt;0&gt; ) I Função ! selecionar tuplas da primeira relação não co I Operação não comutativa R 1 GLYPH&lt;0&gt; R 2 , R 2 GLYPH&lt;0&gt; R 1 Exemplo ! PROFESSOR GLYPH&lt;0&gt; ALUNO PROFESSOR ALUNO DIFERENÇA

| Nome            |   Depto |
|-----------------|---------|
| Roberto Machado |       1 |
| Manuela Costa   |       3 |

| Nome            |   Departamento |
|-----------------|----------------|
| Roberto Machado |              2 |
| Manuela Costa   |              3 |

| Nome            |   Depto |
|-----------------|---------|
| Roberto Machado |       1 |



## Operações DIVISÃO

 CC BY-NC-ND 4.0 eem 2 R 1 GLYPH&lt;4&gt; R 2 I Operador ! dividir ( GLYPH&lt;4&gt; ) I Função ! extrair subconjunto de tuplas de R 1 present R I Relação resultante possui os atributos de R 1 não presentes em R 2 I Relação resultante possui as tuplas de R 1 que contêm as tuplas de R 2 I Operação não comutativa R 1 GLYPH&lt;4&gt; R 2 , R 2 GLYPH&lt;4&gt; R 1



## Operação DIVISÃO

Exemplo ! CARGA GLYPH&lt;4&gt; EXATAS

Encontrar os professores que possuem cargas horárias em todos os cursos da área de ciências exatas

## CARGA

| Professor   | Curso                 |
|-------------|-----------------------|
| Felipe      | Wladmir Administração |
| Max         | Administração         |
| Felipe      | Computação            |
| Max         | Computação            |
| Teldo       | CC Computação         |
| Luiz        | Engenharia            |
| Max         | Engenharia            |



Professor

Max

 CC BY-NC-ND 4.0 EXATAS DIVISÃO



## Referências Bibliográficas

- [1] Elmasri, Ramez; Navathe, Sham. Fundamentals of Database Systems . 7ed. Pearson, 2016.
- [2] Silberschatz, Abraham; Korth, Henry F.; Sudarshan, S. Database System Concepts . 6ed. McGraw-Hill, 2011.
- [3] Date, Christopher J. An Introduction to Database Systems . 8ed. Pearson, 2004.



## Sistemas de Banco de Dados

Fundamentos em Bancos de Dados Relacionais



Material distribuído sob licença CC BY-NC-ND 4.0

Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International

## tecnologias de armazenamento



## Tecnologias de Armazenamento de Dados

 entoeà CC BY-NC-ND 4.0 Desempenho e confiabilidade em sistemas de banco de dados estão intimamente relacionados à organização dos dados nos meios de armazenam tecnologia de armazenamento de dados empregada I Minimizar o número de transferências de blocos e bu ff ers I Agilizar o tempo de cada transferência Organização adequada de dados ajuda a minimizar número de transferências I Tipo de arquivo empregado pode tornar a busca linear, logarítmica ou em tempo constante Tecnologia de armazenamento adequada ajuda a reduzir custo de transferência

- I Tipo de memória secundária empregada, bem como sua configuração, podem acelerar o acesso aos dados em ordens de magnitute



## Hardware de Armazenamento

-  utacional CC BY-NC-ND 4.0 Padrão de interligação de periféricos determina a forma como dispositivos, como memórias secundárias, são interligados ao hardware comp I ATA ( Advanced Technology Attachment ) ! ou IDE ( Integrated Drive Eletronics ) é um padrão que oferece baixos custo e desempenho, suportando velocidade de transferência até GLYPH&lt;25&gt; 0,15Gbps I SATA ( Serial ATA ) ! padrão flexível, oferecendo uma gama de opções com custos variados, suportando velocidade de transferência até GLYPH&lt;25&gt; 6Gbps I SCSI ( Small Computer System Interface ) ! custo e desempenho elevados, suportando velocidade de transferência até GLYPH&lt;25&gt; 6Gbps

Padrões diferem entre si não só quanto à velocidade de transferência, mas também quanto aos recursos suportados, em especial a possibilidade de criação de conjuntos de discos magnéticos (RAID) com hot-swap



## Hardware de Armazenamento





## Conjuntos de Discos

 dadelógica CC BY-NC-ND 4.0 RAID ( Redundant Array of Independent Disks ) é uma tecnologia de virtualização de armazenamento que combina discos em uma uni I Desempenho ! possibilidade de ampliação da capacidade de armazenamento e da velocidade de transferência de dados I Distribuição de dados em vários discos, com balanceamento de carga I I/O paralelo, provendo alta taxa de transferência I Redundância ! possibilidade de ampliação da disponibilidade e da confiabilidade por ser tolerante a falhas I Distribuição de cópias de dados em vários discos

Suporta diferentes esquemas de configuração, provendo diferentes níveis de desempenho e redundância



## Conjuntos de Discos

 CC BY-NC-ND 4.0 1discos RAID 0 Distribuição sem cópia Requisito ! n &gt; Velocidade !/ n Capacidade !GLYPH&lt;17&gt; n Não tolerante a falhas



Alto desempenho, com taxa de falha maior que em discos sem RAID



## Conjuntos de Discos

 CC BY-NC-ND 4.0 1discos RAID 1 Requisito ! n &gt; Velocidade !/ 1 Capacidade !GLYPH&lt;17&gt; 1 Tolerante a falhas



Espelhamento sem distribuição

Desempenho equivalente a discos sem RAID, mas com taxa de falha menor



## Conjuntos de Discos

 CC BY-NC-ND 4.0 2discos RAID 5 Distribuído com cópia Requisito ! n &gt; Velocidade !/ n Capacidade !GLYPH&lt;17&gt; n GLYPH&lt;0&gt; 1 Tolerante a falhas



Desempenho e capacidade próximos ao RAID 0, com taxa de falha menor que discos sem RAID



## Conjuntos de Discos

 CC BY-NC-ND 4.0 RAID 10 Espelhado com distribuição Requisito ! n / m ^ n &gt; m Velocidade !/ n m = Capacidade !GLYPH&lt;17&gt; n m = Tolerante a falhas



Combinação RAID 1 (espelho tamanho m ) e 0, suportando múltiplas falhas, enquanto houver cópia espelhada



## Abordagens de Armazenamento

DAS (Direct-Attached Storage) ! discos magnéticos contendo os arquivos dos bancos de dados integrados ao hardware do sistema de banco de



 dados I Integração por meio de padrões de interligação, como ATA, SATA e SCSI I Discos acessíveis diretamente apenas pelo hardware do sistema

CC BY-NC-ND 4.0

- I Abordagem simples e barata, mas menos robusta e escalável



## Abordagens de Armazenamento

NAS (Network-Attached Storage) ! arquivos de bancos de dados parcial ou totalmente contidos em hardware especializado de compartilham





- I Hardware de sistema de banco de dados "enxerga" hardware especialista como servidor de arquivo

CC BY-NC-ND 4.0

 entodearquivo I Integração por protocolos de compartilhamento, como NFS, SMB e AFP



## Abordagens de Armazenamento

SAN (Storage Area Network) ! rede dedicada, geralmente em fibra óptica, de hardwares de armazenamento e de sistemas de banco de dados





- I Suporta hardware dedicado de armazenamento interligado ao hardware de sistema através da rede



CC BY-NC-ND 4.0

- I Hardware de sistema "enxerga" hardware dedicado como disco



## Abordagens de Armazenamento



- I Hardware de sistema "enxerga" e acessa diretamente discos distribuídos pela rede como se estivessem fisicamente conectados

 iSCSI (Internet SCSI) ! arquivos de bancos de dados parcial ou totalmente contidos em discos espalhados e acessíveis diretamente pela rede I Integração por protocolos de camada de transporte TCP/IP

CC BY-NC-ND 4.0

- I Abordagem flexível, barata e escalável



## Referências Bibliográficas

- [1] Elmasri, Ramez; Navathe, Sham. Fundamentals of Database Systems . 7ed. Pearson, 2016.
- [2] Silberschatz, Abraham; Korth, Henry F.; Sudarshan, S. Database System Concepts . 6ed. McGraw-Hill, 2011.
- [3] Date, Christopher J. An Introduction to Database Systems . 8ed. Pearson, 2004.



## Sistemas de Banco de Dados

Fundamentos em Bancos de Dados Relacionais



Material distribuído sob licença CC BY-NC-ND 4.0

Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International



## Otimização de Consulta

 CC BY-NC-ND 4.0 Escolha de algoritmos e estratégias eficientes para execução de sequências de operações de álgebra relacional I Heurística ! aplicação de regras I Consultas interpretadas I Custo ! estimativa de custo de execução I Consultas compiladas I Semântica ! compreensão e substituição I Consulta é substituída por outra "melhor" Execução do plano tipicamente de forma encadeada ( pipeline ) sem geração de arquivos intermediários





## Árvore de Consulta

CC BY-NC-ND 4.0

 Estrutura em árvore que representa uma expressão de álgebra relacional I Folha ! arquivo de entrada I Interno ! operação da álgebra relacional I Raíz ! operação de projeção final da álgebra relacional I Ordem ! operações executadas da folha esquerda para a raíz





## Otimização Heurística

 CC BY-NC-ND 4.0 deconsultainicial Heurística ! método para modificação da representação interna de uma consulta, visando tornar seu plano de execução eficiente I Não garante que a melhor representação interna, aquela que gere o plano de execução mais eficiente, seja gerada I Aplicação de um conjunto de regras sobre uma árvore I Árvore inicial obtida a partir do parsing da consulta I Operações algébricas que reduzam o tamanho dos resultados intermediários devem ser executadas primeiro I Operações unárias de seleção projeção , e agregação antes de operações binárias de junção , e de conjunto I Operações algébricas de menor custo devem ser executadas primeiro I Operações binárias mais eficientes antes



## Otimização Heurística

ALUNO

A,

PROFESSOR

P

A.CPF

=

P.CPF

P.Sexo

= 'F';



CC BY-NC-ND 4.0

 Árvore Inicial ! o parsing da consulta pode ser feito no sentido natural, da esquerda para a direita, ou reverso, da direita para a esquerda I Arquivos e operações são inseridos na árvore na ordem de parsing SELECT A.CPF, A.Nome FROM WHERE AND



## Otimização Heurística

 CC BY-NC-ND 4.0 Regras ! modificam árvore de consulta inicial, baseando-se no princípio reduzir para combinar I Redução ! operações unárias precedem operações binárias I Primeira operação em cada nó folha deve ser seleção , seguida de projeção , seguida de agregação I Combinação ! operações de menor custo precedem as de custo maior I Nós folhas devem ser reordenados de forma que junções mais eficientes sejam executadas primeiro, evitando-se produtos cartesianos



## Otimização Heurística

 CC BY-NC-ND 4.0 Considerando parsing no sentido reverso, e existência de índice multinível em CPF de professor e aluno , e índice primário em Numero de departamento : SELECT D.Nome, A.CPF FROM ALUNO A, DEPARTAMENTO D, PROFESSOR P WHERE A.CPF = P.CPF AND A.Sexo = 'F' AND P.Depto = D.Numero AND P.Salario &gt; 5.000,00 Z P Depto : P Salario : &gt; :





## Otimização Heurística

Projeções internas reduzem ainda mais o tamanho dos resultados intermediários





Consulta pode ser reescrita de forma que a árvore inicial resultante do parsing se aproxime da árvore de consulta otimizada 



## Otimização Heurística

Plano de Execução ! métodos de acesso, algoritmos e estratégias usados no processamento das operações na árvore de consulta otimizada



- 1. Pesquisa Linear ! arquivo não indexado A
- 2. Pesquisa Linear ! arquivo não indexado P
- 3. Junção de loop único ! varre arquivo não indexado A e pesquisa arquivo de índice de P
- 4. Junção de loop único ! varre resultado intermediário e pesquisa arquivo de índice de D

CC BY-NC-ND 4.0





## Otimização Baseada em Custo

 va CC BY-NC-ND 4.0 to Função de Custo ! computa estimativa de custo para algumas estratégias de execução de consulta, escolhendo a estratégia de menor estimati I Tempo de Resposta ! # estratégias de execução avaliadas é limitado I Consultas Compiladas ! otimização feita na compilação I Evidências de Custo ! combinadas pela função de cus I Computação ! custo de processamento (CPU) de dados em memória primária I Memória ! consumo de bu ff ers de memória primária I Disco ! consumo de blocos de disco I I/O ! custo com operações de paginação, transferência de dados entre memória primária e secundária I Comunicação ! custo de transferência de dados via rede



## Otimização Baseada em Custo

 CC BY-NC-ND 4.0 Catálogo ! armazena informação necessária para estimar custo I Arquivo ! organização, tamanho, blocagem, # blocos, tamanho de registro, # de registros I Índice ! tipo, # níveis, # blocos em 1 GLYPH&lt;14&gt; nível I Registro ! distribuição de valores I Seletividade ! fração de registros que satisfazem uma condição de igualdade em um campo I Exemplo ! 50% de registros de professor tem Sexo = 'M' I Cardinalidade ! # médio de registros que satisfazem uma condição de associação por igualdade em um campo

- I Exemplo ! cada registro de departamento está associado em média a 5 registros de professor



## Otimização Semântica

Forma que demanda junção por loop único se professor ou aluno tiverem índice em CPF

 iente CC BY-NC-ND 4.0 Compreensão ! SGBD precisa compreender o significado da consulta para reescrevêla de uma forma melhor , que gere um plano de execução mais efic A seguinte consulta demanda força bruta para execução: SELECT CPF, Nome FROM PROFESSOR WHERE CPF IN (SELECT CPF FROM ALUNO) Mas pode ser reescrita para: SELECT A.CPF, A.Nome FROM PROFESSOR A, ALUNO B WHERE A.CPF = B.CPF



## Referências Bibliográficas

- [1] Elmasri, Ramez; Navathe, Sham. Fundamentals of Database Systems . 7ed. Pearson, 2016.
- [2] Silberschatz, Abraham; Korth, Henry F.; Sudarshan, S. Database System Concepts . 6ed. McGraw-Hill, 2011.
- [3] Date, Christopher J. An Introduction to Database Systems . 8ed. Pearson, 2004.



## Sistemas de Banco de Dados

Fundamentos em Bancos de Dados Relacionais



Material distribuído sob licença CC BY-NC-ND 4.0

Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International

## processamento de consulta



## Processamento de Consulta

## SGBDs processam otimizam , e executam consultas



 CC BY-NC-ND 4.0 ticaisSQL I Parsing ! análise sintática I Varredura ! tokenização I Análise ! regras grama I Validação ! metadados 2 esquema I Otimização ! escolha de estratégia eficiente para execução da consulta I Árvore de Consulta ! ou grafo de consulta é uma representação interna da consulta I Plano de Execução ! estratégia de execução

- I Geração de Código ! código compilado ou interpretado para execução



## Processamento de Consulta: Tradução

CC BY-NC-ND 4.0

WHERE

Sexo = 'M';

 Parsing ! consulta é traduzida para álgebra relacional I Tradução ! decomposição em blocos de expressões SELECT-FROM-WHERE SELECT CPF, Nome FROM PROFESSOR WHERE Salario &gt; (SELECT AVG(Salario) FROM PROFESSOR WHERE Sexo='M'); SELECT CPF, Nome FROM PROFESSOR WHERE Salario &gt; X; Æ CPF Nome ; ( ª Salario &gt; X ( PROFESSOR )) SELECT AVG(Salario) FROM PROFESSOR GLYPH&lt;213&gt; AVG Salario ( ) ( ª Sexo = 0 M 0 ( PROFESSOR ))



## Processamento de Consulta: Algoritmos

 lacional CC BY-NC-ND 4.0 Processar uma consulta envolve a escolha de algoritmos e estratégias a serem aplicados na execução de sequências de operações da álgebra re I Ordenação ! agregação conjunto junção , , e projeção ( distinct ) I Pesquisa ! junção e seleção I Hashing ! agregação conjunto junção projeção , , , e seleção A escolha do algoritmo e estratégia adequados é feita pelo SGBD, dependendo da tecnologia de armazenamento e da organização de dados I Memória primária livre ! hashing em operação de junção I Arquivo ordenado ! pesquisa binária em operação de seleção



## Algoritmos: Ordenação Externa

CC BY-NC-ND 4.0

 Estratégia de ordenação e intercalação ( merge-sort ) de registros em disco I Ordenação ! partes ( runs ) do arquivo são transferidas do disco para memória primária, ordenadas em memória primária e regravadas em disco I BM ! # bu ff ers disponíveis em memória primária I BD ! # blocos do arquivo em disco I R = l BD BM m ! # runs I Intercalação ! mesclagem de runs ordenadas em disco I Grau ! D = min (( BM GLYPH&lt;0&gt; 1 ) ; R ) ! # runs mescladas em cada passo I S = d log D R e ! # passos de intercalação

Custo O n ( log n ) ! ( 2 GLYPH&lt;2&gt; BD ) + ( 2 GLYPH&lt;2&gt; BD GLYPH&lt;2&gt; d log D R e )



## Algoritmos: Ordenação Externa

Exemplo de merge-sort com 24 registros em 12 blocos e 3 bu ff ers , realizando ordenação em d 12 3 = e = 4 runs e intercalação de grau 2 em d log 2 4 e = 2 passos







## Algoritmos: Ordenação Externa

CC BY-NC-ND 4.0

 Para ordenar um arquivo que ocupa 1024 blocos em disco usando 5 bu ff ers : I Ordenação ! 205 runs ordenadas em disco I R = l 1024 5 m = d 204 8 ; e = 205 I Intercalação ! grau 4 em 4 passos I D = min (( 5 GLYPH&lt;0&gt; 1 ) ; 205 ) = 4 I S = d log 4 205 e GLYPH&lt;25&gt; d 3 84 ; e = 4 I Passo 1 ! 205 runs mescladas 4 a 4 I Passo 2 ! 52 runs mescladas 4 a 4 I Passo 3 ! 13 runs mescladas 4 a 4 I Passo 4 ! 4 runs mescladas

Custo ! ( 2 GLYPH&lt;2&gt; 1024 ) + ( 2 GLYPH&lt;2&gt; 1024 GLYPH&lt;2&gt; 4 ) = 10 240 :



## Algoritmos: Projeção ( Æ )

## Estratégias envolvem eliminar registros duplicados

- I Ordenação-Intercalação ! O n ( log n )
- I Ordena-se o resultado da projeção e varre-se sequencialmente registros removendo duplicatas em registros adjacentes
- I Hashing ! O n ( )
- CC BY-NC-ND 4.0 I Computa-se um endereço de partição ( bucket ) a partir de uma função hash sobre cada registro de resultado, alocando-o no bucket correspondente I Antes da alocação verifica-se se o registro já está presente no bucket , somente alocando-o se não estiver presente







## Algoritmos: Seleção ( ª )

CC BY-NC-ND 4.0

- I Condição de seleção envolve comparação de = em campo hash

 Inúmeras estratégias possíveis, dependendo da existência de índices e da característica e complexidade da condição de seleção I Arquivo Não Indexado I Pesquisa Linear ! O n ( ) I Recupera-se cada registro e verifica-se se valores em campos satisfazem a condição de seleção I Pesquisa Binária ! O ( log n ) I Condição de seleção envolve comparação de &lt; GLYPH&lt;20&gt; = GLYPH&lt;21&gt; &gt; em campo de ordenação I Hashing ! O ( 1 )



## Algoritmos: Seleção ( ª )

CC BY-NC-ND 4.0

 I Arquivo Indexado I Índice Primário, de Agrupamento, Secundário ou Multinível ! O ( log n ) I Condição de seleção envolve comparação de &lt; GLYPH&lt;20&gt; = GLYPH&lt;21&gt; &gt; em campo de indexação I Índice Hash ! O ( 1 ) I Condição de seleção envolve comparação de = em campo de indexação I Seleção Conjuntiva ! operador ^ na condição de seleção I Índice Composto ! O ( log n ) I Condição de seleção envolve um subconjunto dos campos de indexação, desde que todos os campos iniciais estejam presentes



## Algoritmos: Seleção ( ª )

CC BY-NC-ND 4.0

- I Pesquisa-se em cada índice secundário separadamente e realiza-se a união de ponteiros recuperados. Demanda índice para cada campo na condição de seleção

 I Seleção Conjuntiva ! operador ^ na condição de seleção I Índice Individual ! O ( log n ) I Pesquisa-se no índice e verifica-se condições remanescentes da seleção I Índice Múltiplo ! O ( log n ) I Pesquisa-se em cada índice secundário separadamente, realiza-se a intersecção de ponteiros recuperados, e verifica-se condições remanescentes da seleção I Seleção Disjuntiva ! operador \_ na condição de seleção I Índice Múltiplo ! O ( log n )



## Algoritmos: Operações de Conjunto ( GLYPH&lt;2&gt; [ \GLYPH&lt;0&gt; )

## Estratégias envolvem combinação de registros

 CC BY-NC-ND 4.0 I Força Bruta ! O n ( 2 ) I Produto Cartesiano ( GLYPH&lt;2&gt; ) ! combinam-se todos os registros de cada conjunto I Ordenação-Intercalação ! O n ( log n ) I Ordenam-se os registros dos dois conjuntos, varrem-se os dois conjuntos simultâneamente e a operação de conjunto apropriada é efetuada I Hashing ! O n ( ) I Computam-se endereços de bucket a partir de uma função hash para alocação de registros do menor conjunto I Computa-se a função hash para cada registro do outro conjunto

- I Aloca-se ( união ) ou desaloca-se ( diferença ou intersecção ) o registro no bucket correspondente de acordo com a operação de conjunto utilizada



## Algoritmos: Agregação ( GLYPH&lt;213&gt; )

CC BY-NC-ND 4.0 ãodeagregação

 Estratégias dependem da existência de índices e de campos de agrupamento I Completa ! campo de agrupamento ( group by ) não especificado I O n ( ) ! varre-se arquivo de dados ou de índice computando função I O ( log n ) ! para índice B+ Tree no campo usado na funç I Particionada ! campo de agrupamento ( group by ) especificado I Ordenação ! O n ( log n ) I Ordena-se arquivo pelo campo de agrupamento, varrendo-o e computando função de agregação para cada partição I Hashing ! O n ( ) I Particiona-se o arquivo em buckets usando campo de agrupamento e computa-se função de agregação para cada bucket

- I Índice de Agrupamento ! O n ( )
- I Arquivo já particionado, bastando computar função de agregação



## Algoritmos: Junção ( Z )

CC BY-NC-ND 4.0

 Estratégias dependem da existência de índices e da característica e complexidade da condição de junção I Junção de Loop Aninhado ! O n ( 2 ) I Força bruta I Para cada registro r i 2 R , recuperar cada registro sj 2 S I Combinar r i e sj se satisfazem a condição de junção I Junção de Loop Único ! O n ( log n ) I Aplicável caso haja índice em ao menos um arquivo I Para cada registro r i 2 R , onde R é o arquivo com maior custo de busca

- I Usar o índice em S para recuperar os registros que satisfazem a condição de junção, combinando-os com o registro r i



## Algoritmos: Junção ( Z )

 CC BY-NC-ND 4.0 nção I Junção Ordenação-Intercalação ! O n ( log n ) I Ordena-se arquivos por campos presentes na condição de junção I Varrem-se simultâneamente ambos os arquivos pelo campo de ordenação, combinando os registros que satisfazem a condiçào de ju I Registros em cada arquivo são acessados apenas uma vez I Junção Hash ! O n ( ) I Para condição de junção com comparação de = I Varre-se o arquivo R de menor tamanho, aplicando uma função hash sobre o campo presente na condição de junção para criar buckets em memória

- I Para cada registro em S , use a função hash para encontrar registros em R que satisfazem a condiçào de junção, e combine-os com o registro de S



## Algoritmos: Junção Externa ( on [ )

CC BY-NC-ND 4.0

 Estratégia envolve a combinação de estratégias de junção e de conjunto 1. Junte os arquivos R e S usando a melhor estratégia de junção 2. Use a operação diferença para encontrar os registros do arquivo R (aberto) não presentes no resultado da junção 3. Produto cartesiano dos registros não presentes de R com registro NULO de S 4. Use a operação união para combinar os registros das etapas 1 e 3 Custo ! ( Z ) + ( GLYPH&lt;0&gt; ) + ( GLYPH&lt;2&gt; ) + ( [ )



## Referências Bibliográficas

- [1] Elmasri, Ramez; Navathe, Sham. Fundamentals of Database Systems . 7ed. Pearson, 2016.
- [2] Silberschatz, Abraham; Korth, Henry F.; Sudarshan, S. Database System Concepts . 6ed. McGraw-Hill, 2011.
- [3] Date, Christopher J. An Introduction to Database Systems . 8ed. Pearson, 2004.



## Sistemas de Banco de Dados

Fundamentos em Bancos de Dados Relacionais



Material distribuído sob licença CC BY-NC-ND 4.0

Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International

## álgebra relacional i



## Álgebra Relacional

CC BY-NC-ND 4.0

 Conjunto de operações para manipulação de BD relacionais I Linguagem formal para o modelo relacional I Consulta ! solicitação de recuperação de dados especificada por uma sequência de operações algébricas I Resultado de uma consulta é uma nova relação I SQL incorpora seus principais conceitos I SQL ! linguagem de consulta prática para BD relacionais I Multiplicidade de operações: I Unárias ! aplicadas sobre uma relação I Binárias ! aplicadas sobre duas relações I Agregação ! resumem dados de relações



## Operação SELEÇÃO



 CC BY-NC-ND 4.0 amaumacondição ª condicional ( R ) I Operador ! selecionar ( ª sigma ) I Função ! filtrar tuplas de uma relação R que satisfaç I Tuplas que não satisfazem a condição são descartadas do resultado I Relação resultante tem os mesmos atributos de R I Número de tuplas na relação resultante é menor ou igual ao número de tuplas em R





## Operação SELEÇÃO

|

&lt;atributo&gt; &lt;operador&gt; &lt;atributo&gt;

&lt;

 Condição de seleção é uma expressão booleana &lt;atributo&gt; &lt;operador&gt; &lt;valor&gt; I &lt;atributo&gt; ! nome de um atributo de R I &lt;operador&gt; ! operador de comparação I &lt;valor&gt; ! constante do domínio do atributo

GLYPH&lt;20&gt;

=

GLYPH&lt;21&gt;

&gt;

,

Conectada por operadores booleanos ( ^ \_ : ) formam um único bloco condicional

CC BY-NC-ND 4.0





## Operação SELEÇÃO

|         CPF | Nome              | Sexo   |   Salario |   4.0 Departamento |
|-------------|-------------------|--------|-----------|--------------------|
| 12345678900 | Roberto Machado   | M      |      1200 |                  1 |
| 12345678901 | Manuela Costa     | F      |      2700 |                  3 |
| 21345678900 | Carlos A. Martins | M      |      3200 |                  1 |
| 32145678900 | Ana Maria Freitas | F      |      7500 |                  2 |

CC BY-NC-ND 4.0 mento

 Exemplo ! selecionar tuplas de professores do sexo feminino ª Sexo = 0 F 0 ( PROFESSOR ) PROFESSOR



## Operação SELEÇÃO

Exemplo ! selecionar tuplas de professores do sexo masculino que recebem salário maior que 3000,00

|         CPF | Nome                       | Sexo   |   Salario |   Departamento |
|-------------|----------------------------|--------|-----------|----------------|
| 12345678900 | Roberto Machado            | M      |      1200 |              1 |
| 12345678901 | Manuela Costa              | F      |      2700 |              3 |
| 21345678900 | Carlos A. Martins          | M      |      3200 |              1 |
| 32145678900 | BY-NC-ND Ana Maria Freitas | F      |      7500 |              2 |

CC BY-NC-ND 4.0

 ª ( Sexo = 0 M 0 ^ Salario &gt; 3000 00 : ) ( PROFESSOR ) PROFESSOR



## Operação SELEÇÃO

 nteenãose CC BY-NC-ND 4.0 I Condições de seleção são aplicadas a cada tupla individualme aplicam a mais de uma tupla I Operação unária e comutativa ª cond 1 ( ª cond 2 ( R )) = ª cond 2 ( ª cond 1 ( R )) I Pode-se combinar uma sequência de operações em uma única operação com operadores conjuntivos ª cond 1 ( ª cond 2 ( ::: ( ª condn ( R )) ::: )) = ª cond 1 ^ cond 2 ^ ::: ^ condn ( R )



## Operação PROJEÇÃO



 CC BY-NC-ND 4.0 Æ atributos ( R ) I Operador ! projetar ( Æ pi ) I Função ! filtrar atributos de uma relação R I Atributos não especificados são descartados do resultado I Relação resultante possui um subconjunto de atributos de R explicitamente especificados e na mesma ordem I Número de tuplas na relação resultante é menor ou igual ao número de tuplas em R

- I Menor se houverem tuplas duplicadas, pois duplicatas são eliminadas



## Operação PROJEÇÃO

## Exemplo ! projetar nome e salário de professores

|         CPF | Nome              | Sexo   |   Salario |   4.0 Departamento |
|-------------|-------------------|--------|-----------|--------------------|
| 12345678900 | Roberto Machado   | M      |      1200 |                  1 |
| 12345678901 | Manuela Costa     | F      |      2700 |                  3 |
| 21345678900 | Carlos A. Martins | M      |      3200 |                  1 |
| 32145678900 | Ana Maria Freitas | F      |      7500 |                  2 |

CC BY-NC-ND 4.0 mento

 Æ Nome Salario ; ( PROFESSOR ) PROFESSOR



## Operação PROJEÇÃO

|         CPF | Nome              | Sexo   |   Salario |   4.0 Departamento |
|-------------|-------------------|--------|-----------|--------------------|
| 12345678900 | Roberto Machado   | M      |      1200 |                  1 |
| 12345678901 | Manuela Costa     | F      |      2700 |                  3 |
| 21345678900 | Carlos A. Martins | M      |      3200 |                  1 |
| 32145678900 | Ana Maria Freitas | F      |      7500 |                  2 |

CC BY-NC-ND 4.0 mento

 Exemplo ! projetar número do departamento e sexo de professores Æ Departamento ; Sexo ( PROFESSOR ) PROFESSOR Duas tuplas repetidas ( &lt; 1, M &gt; ) no resultado, uma delas será eliminada



## Operação PROJEÇÃO

 ,arelação CC BY-NC-ND 4.0 I Se a lista de atributos para projeção inclui a chave da relação R resultante terá o mesmo número de tuplas de R I Operação unária , mas não comutativa Æ atr 1 ( Æ atr 2 ( R )) , Æ atr 2 ( Æ atr 1 ( R )) I Aninhamento de sequência de operações válidas equivale à operação externa do aninhamento

<!-- formula-not-decoded -->



## Sequência de Operações

 CC BY-NC-ND 4.0 Consultas combinam sequências de operações algébricas I Expressão em Linha ! aninha-se múltiplas operações, gerando uma única expressão algébrica Æ CPF ; Nome Salario ; ( ª Sexo = 0 F 0 ( PROFESSOR ) ) I Relacões Intermediárias ! aplica-se uma operação de cada vez, criando relações com resultados intermediários reutilizáveis A GLYPH&lt;0&gt; ª Sexo = 0 F 0 ( PROFESSOR ) B GLYPH&lt;0&gt; Æ CPF ; Nome Salario ; ( A )



## Operação RENOMEAR

- I Operador ! renomear ( GLYPH&lt;226&gt; rho )
- I GLYPH&lt;226&gt; atributos ( R ) ! renomeia apenas atributos

 GLYPH&lt;226&gt; S atributos ( ) ( R )

- CC BY-NC-ND 4.0 I Função ! renomear relações e atributos I S ! nome da relação resultante I atributos ! lista dos novos nomes dos atributos de R na relação resultante, ordem na lista deve ser compatível com ordem dos atributos de R I Variações:
- I GLYPH&lt;226&gt; S ( R ) ! renomeia apenas relação



## Operação RENOMEAR

|         CPF | Name              | Gender   |   Salary |   4.0 DNum |
|-------------|-------------------|----------|----------|------------|
| 12345678900 | Roberto Machado   | M        |     1200 |          1 |
| 12345678901 | Manuela Costa     | F        |     2700 |          3 |
| 21345678900 | Carlos A. Martins | M        |     3200 |          1 |
| 32145678900 | Ana Maria Freitas | F        |     7500 |          2 |

CC BY-NC-ND 4.0 um

 Exemplo ! renomear a relação professor e seus respectivos atributos GLYPH&lt;226&gt; TEACHER CPF Name Gender Salary DNum ( ; ; ; ; ) ( PROFESSOR ) TEACHER



## Operação RENOMEAR

 Alternativamente, pode-se renomear relações e atributos utilizando relações intermediárias TEACHER CPF Name Gender Salary ( ; ; ; ; DNum ) GLYPH&lt;0&gt; PROFESSOR TEACHER Name Salary ( ; ) GLYPH&lt;0&gt; Æ Nome Salario ; ( PROFESSOR ) MAN CPF Nom Sex Sal ( ; ; ; ; DNum ) GLYPH&lt;0&gt; ª Sexo = 0 M 0 ( PROFESSOR )

Pode-se renomear qualquer subconjunto de atributos de R

CC BY-NC-ND 4.0





## Operação PRODUTO

 CC BY-NC-ND 4.0 R 1 GLYPH&lt;2&gt; R 2 I Operador ! multiplicar ( GLYPH&lt;2&gt; ) I Função ! combinar tuplas de duas relações I Relação resultante possui os atributos de R 1 e R 2, incluindo como tuplas todas as combinações possíveis entre as tuplas de R 1 e R 2 I Número de tuplas da relação resultante é o produto cartesiano entre o número de tuplas de R 1 e R 2



## Operação PRODUTO

## Exemplo ! PROFESSOR GLYPH&lt;2&gt; DEPARTAMENTO

|         CPF | Nome    | Sexo   |   Salario |   Departamento |
|-------------|---------|--------|-----------|----------------|
| 12345678900 | Roberto | M      |      1200 |              1 |
| 12345678901 | Manuela | F      |      2700 |              3 |

## Resultado:

CC BY-NC-ND 4.0 Tecnologia

|   Numero | Nome           |
|----------|----------------|
|        1 | Administrativo |
|        2 | Comercial      |
|        3 | Tecnologia     |

|         CPF | Nome       | Sexo   |   Salario |   Departamento |   Numero | Nome           |
|-------------|------------|--------|-----------|----------------|----------|----------------|
| 12345678900 | Roberto    | M      |      1200 |              1 |        1 | Administrativo |
| 12345678900 | Roberto    | M      |      1200 |              1 |        2 | Comercial      |
| 12345678900 | Roberto    | M      |      1200 |              1 |        3 | Tecnologia     |
| 12345678901 | CC Manuela | F      |      2700 |              3 |        1 | Administrativo |
| 12345678901 | Manuela    | F      |      2700 |              3 |        2 | Comercial      |
| 12345678901 | Manuela    | F      |      2700 |              3 |        3 | Tecnologia     |

 PROFESSOR DEPARTAMENTO



## Operação PRODUTO

## Associada à SELEÇÃO opera como uma JUNÇÃO

|         CPF | Nome    | Sexo   |   Salario |   Departamento |
|-------------|---------|--------|-----------|----------------|
| 12345678900 | Roberto | M      |      1200 |              1 |
| 12345678901 | Manuela | F      |      2700 |              3 |

## Resultado:

|   4.0 Numero | Nome           |
|--------------|----------------|
|            1 | Administrativo |
|            2 | Comercial      |
|            3 | Tecnologia     |

|         CPF | Nome    | Sexo   |   Salario |   Departamento |   Numero | Nome           |
|-------------|---------|--------|-----------|----------------|----------|----------------|
| 12345678900 | Roberto | M      |      1200 |              1 |        1 | Administrativo |
| 12345678901 | Manuela | F      |      2700 |              3 |        3 | Tecnologia     |

CC BY-NC-ND 4.0

 ª Departamento = Numero ( PROFESSOR GLYPH&lt;2&gt; DEPARTAMENTO ) PROFESSOR DEPARTAMENTO



## Operação JUNÇÃO

 CC BY-NC-ND 4.0 eumacondição R 1 Z condicional R 2 I Operador ! juntar ( Z ) I Função ! combinar tuplas de duas relações a partir d I Relação resultante possui atributos de R 1 e R 2, incluindo como tuplas todas as combinações entre as tuplas de R 1 e R 2 que respeitam condição I Tuplas que não respeitam condição de junção ou que valores dos atributos usados na condição sejam NULL são descartadas do resultado



## Operação JUNÇÃO

|         CPF | Nome    | Sexo   |   Salario |   Departamento |
|-------------|---------|--------|-----------|----------------|
| 12345678900 | Roberto | M      |      1200 |              1 |
| 12345678901 | Manuela | F      |      2700 |              3 |

|   Numero | Nome           |
|----------|----------------|
|        1 | Administrativo |
|        2 | Comercial      |
|        3 | Tecnologia     |

|         CPF | Nome    | Sexo   |   Salario |   Departamento |   Numero | Nome           |
|-------------|---------|--------|-----------|----------------|----------|----------------|
| 12345678900 | Roberto | M      |      1200 |              1 |        1 | Administrativo |
| 12345678901 | Manuela | F      |      2700 |              3 |        3 | Tecnologia     |

CC BY-NC-ND 4.0

 Exemplo ! PROFESSOR Z Departamento = Numero DEPARTAMENTO PROFESSOR DEPARTAMENTO Resultado:



## Operação JUNÇÃO

|         CPF | Nome       | Sexo   |   Salario |   Departamento |
|-------------|------------|--------|-----------|----------------|
| 12345678900 | Roberto    | M      |      1200 |              1 |
| 12345678901 | CC Manuela | F      |      2700 |              3 |

 CC BY-NC-ND 4.0 Equijunção ! condicionais com operadores de igualdade PROFESSOR Z Departamento = Numero DEPARTAMENTO Junção Natural ! equijunção automática (natural) com atributos que possuem o mesmo nome nas duas relações removendo-se duplicatas PROFESSOR GLYPH&lt;3&gt; DEPARTAMENTO PROFESSOR DEPARTAMENTO

|   Numero | Nome           |
|----------|----------------|
|        1 | Administrativo |
|        2 | Comercial      |
|        3 | Tecnologia     |



## Operação JUNÇÃO

CC BY-NC-ND 4.0

 Frequentemente relações diferentes possuem atributos com mesmo nome I Operação RENOMEAR deve ser utilizada antes da junção para evitar problemas de ambiguidade Exemplo: A Numero ( ; DNome ) GLYPH&lt;0&gt; Æ Numero ; Nome ( DEPARTAMENTO ) RESULTADO GLYPH&lt;0&gt; PROFESSOR Z Departamento = Numero A RESULTADO

|         CPF | Nome       | Sexo   |   Salario |   Departamento |   Numero | DNome          |
|-------------|------------|--------|-----------|----------------|----------|----------------|
| 12345678900 | CC Roberto | M      |      1200 |              1 |        1 | Administrativo |
| 12345678901 | Manuela    | F      |      2700 |              3 |        3 | Tecnologia     |



## Operação AGREGAÇÃO



- I Tuplas com valores NULL nos atributos usados na função de agregação são descartadas da agregação
-  CC BY-NC-ND 4.0 malistadeatributos atributos GLYPH&lt;213&gt; funcoes ( R ) I Operador ! agregar ( GLYPH&lt;213&gt; gamma ) I Função ! agregar tuplas de uma relação a partir de u ( atributos de agregação ), aplicando funções de agregação em atributos remanescentes I Múltiplas notações ! F , G I Relação resultante possui atributos de agregação e um atributo para cada função de agregação



## Operação AGREGAÇÃO

 CC BY-NC-ND 4.0 nafunção Função de Agregação ! função matemática aplicada em tuplas agrupadas I COUNT ! conta o número de tuplas agrupadas I SUM ! soma valores do atributo utilizado na função I AVG ! calcula média dos valores do atributo utilizado I MIN ! captura valor mínimo dentre valores do atributo utilizado na função I MAX ! captura valor máximo dentre valores do atributo utilizado na função Se função de agregação não for renomeada, nome do atributo resultante será concatenação do nome da função e do nome do atributo usado por ela 



## Operação AGREGAÇÃO

|         CPF | Nome                      | Sexo   |   Salario | Departamento   |
|-------------|---------------------------|--------|-----------|----------------|
| 12345678900 | Roberto Machado           | M      |      1200 | 1              |
| 12345678901 | Manuela Costa             | F      |      2700 | 3              |
| 21345678900 | Carlos A. Martins         | M      |      3200 | 1              |
| 32145678900 | Cardoso Ana Maria Freitas | F      |      7500 | 4.0 2          |

4

14600.00



 CC BY-NC-ND 4.0 Exemplo ! apresentar o número de professores e o total em salários PROFESSOR GLYPH&lt;213&gt; COUNT CPF ( ) ; SUM Salario ( ) ( PROFESSOR ) Resultado: COUNT\_CPF SUM\_SALARIO



## Operação AGREGAÇÃO

|         CPF | Nome                      | Sexo   |   Salario | Departamento   |
|-------------|---------------------------|--------|-----------|----------------|
| 12345678900 | Roberto Machado           | M      |      1200 | 1              |
| 12345678901 | Manuela Costa             | F      |      2700 | 3              |
| 21345678900 | Carlos A. Martins         | M      |      3200 | 1              |
| 32145678900 | Cardoso Ana Maria Freitas | F      |      7500 | 4.0 2          |

| Sexo   |   SUM_SALARIO |   AVG_SALARIO |
|--------|---------------|---------------|
| F      |         10200 |          5100 |
| M      |          4400 |          2200 |

 CC BY-NC-ND 4.0 Exemplo ! apresentar o total e a média salarial por sexo PROFESSOR Sexo GLYPH&lt;213&gt; SUM Salario ( ) ; AVG Salario ( ) ( PROFESSOR ) Resultado: SUM\_SALARIO AVG\_SALARIO



## Referências Bibliográficas

- [1] Elmasri, Ramez; Navathe, Sham. Fundamentals of Database Systems . 7ed. Pearson, 2016.
- [2] Silberschatz, Abraham; Korth, Henry F.; Sudarshan, S. Database System Concepts . 6ed. McGraw-Hill, 2011.
- [3] Date, Christopher J. An Introduction to Database Systems . 8ed. Pearson, 2004.





## Sistemas de Banco de Dados

Fundamentos em Bancos de Dados Relacionais



Material distribuído sob licença CC BY-NC-ND 4.0

Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International

## armazenamento em memória



## Armazenamento em Memória

CC BY-NC-ND 4.0

 BDs são armazenados fisicamente em meios (mídias) de armazenamento computacional I Meios de armazenamento formam uma hierarquia , em que dados residem e transitam, sendo que a hierarquia reflete a distância do meio à CPU I Memória primária ! próxima e operada diretamente pela CPU I Memória secundária ! distante e não operada pela CPU I Memória terciária ! muito distante e não operada pela CPU I Programas residem e são executados em memória primária I BDs são geralmente grandes e persistem em memória secundária

- I SGBD transfere partes do BD entre memórias de acordo com a necessidade



## Armazenamento em Memória

Existe uma correlação entre capacidade de armazenamento, velocidade de transferência e custo em meios de armazenamento

- I Capacidade de armazenamento ! quantidade de dados (bytes) que podem ser armazenados na memória
- CC BY-NC-ND 4.0 its)quepodemser I Velocidade de transferência ! quantidade de dados (b transferidos de ou para a memória por unidade de tempo (segundo) I Custo ! unidade monetária ($) por quantidade de dados (bytes) que podem ser armazenados na memória Correlação: I &gt; capacidade ) &lt; velocidade


- &gt; armazenamento &lt; velocidade
- &gt; velocidade &gt; custo





## Hierarquia de Memória







## Hierarquia de Memória

 CC BY-NC-ND 4.0 Registrador Memória eletrônica Interna da CPU Rápida !GLYPH&lt;25&gt; 60 Tbps Pequena ! centenas de bytes Cara ! &gt; 500 R$/MB



Utilizada para execução de instruções de programa



## Hierarquia de Memória

 CC BY-NC-ND 4.0 0aL4 Cache Memória eletrônica Vários níveis ! L Rápida ! L1 GLYPH&lt;25&gt; 6 Tbps Pequena ! L4 GLYPH&lt;25&gt; 128 MB Cara ! L0 &gt; 100 R$/MB



Acelera a execução de instruções de programa (pré-busca e pipelining )



## Hierarquia de Memória

 CC BY-NC-ND 4.0 RAM Memória eletrônica Acesso aleatório Rápida !GLYPH&lt;25&gt; 80 Gbps Pequena ! dezenas de GB Cara !GLYPH&lt;25&gt; 0,05 R$/MB



Utilizada para manter instruções de programa e dados temporários



## Hierarquia de Memória

##  CC BY-NC-ND 4.0 ável Flash Memória eletrônica Resistente e dur Rápida !GLYPH&lt;25&gt; 5 Gbps Média ! alguns TB Barata !GLYPH&lt;25&gt; 0,0007 R$/MB



Utilizada para manter dados de maneira persistente



## Hierarquia de Memória

 CC BY-NC-ND 4.0 tação HD Memória magnética Discos em alta ro Lenta !GLYPH&lt;25&gt; 100 Mbps Grande ! dezenas de TB Barata !GLYPH&lt;25&gt; 0,0002 R$/MB



Utilizada para manter dados de maneira persistente



## Hierarquia de Memória

 CC BY-NC-ND 4.0 ial Fita Memória magnética removível Acesso sequenc Lenta !GLYPH&lt;25&gt; 2 Mbps Grande ! PB (jukebox) Barata !GLYPH&lt;25&gt; 0,00003 R$/MB



Utilizada para manter dados pouco mutáveis e acessados de maneira persistente, como backups



## Hierarquia de Memória

 CC BY-NC-ND 4.0 Óptica Memória removível Discos ópticos Lenta !GLYPH&lt;25&gt; 20 Mbps Grande ! PB (jukebox) Barata !GLYPH&lt;25&gt; 0,0001 R$/MB



Utilizada para manter dados pouco mutáveis e de acesso sequencial de maneira persistente, como multimídia



## Hierarquia de Memória

Comparativo entre diferentes tipos de memória:

| Tipo       | Nome        | Cardoso Velocidade (bps)   | Capacidade   | Custo (R$/MB)   | Volátil   |
|------------|-------------|----------------------------|--------------|-----------------|-----------|
| CPU        | Registrador | 60T                        | KB           | 500             | sim       |
| Primária   | Cache       | 6T                         | MB           | 100             | sim       |
| Primária   | RAM         | 80G                        | GB           | 0,05            | sim       |
| Secundária | Flash       | 5G                         | TB           | 4.0 0,0007      | não       |
| Secundária | HD          | 100M                       | TB           | 0,0002          | não       |
| Terciária  | Óptico      | 20M                        | PB           | 0,0001          | não       |
| Terciária  | Fita        | 2M                         | PB           | 0,00003         | não       |



Os valores de velocidade, capacidade e custo são estimativas, a fim de fornecer uma ordem de grandeza. Estimativas foram baseadas em memórias disponíveis atualmente, podendo variar de acordo com a tecnologia e o fabricante

CC BY-NC-ND 4.0 100





## Armazenamento em Memória

Em sistemas de banco de dados, os dados são efetivamente armazenados em diferentes tipos de memória de acordo com sua natureza

- I Transientes ! persistem em memória por um período limitado de tempo, apenas durante a execução do programa
- I No projeto físico , DBAs e projetistas devem escolher as melhores técnicas de organização de dados para garantir equilíbrio entre custo e desempenho, atendendo aos requisitos funcionais e operacionais do BD
- CC BY-NC-ND 4.0 I Persistentes ! permanecem em memória por longos períodos de tempo, sendo acessados e processados repetidamente durante esse período SGBDs devem ser capazes de gerenciar eficientemente a transferência de dados transientes e permanentes entre memórias





## Armazenamento em Memória

CC BY-NC-ND 4.0 damente

 irque: Aplicações tipicamente necessitam de apenas uma pequena parte do BD de cada vez para processamento, sendo responsabilidade do SGBD garant 1. A parte seja transferida da memória secundária para a primária 2. A CPU processe os dados em memória primária adequa 3. Os dados processados sejam transferidos de volta à memória secundária





## Armazenamento em Memória

-  CC BY-NC-ND 4.0 Tipicamente BDs são armazenados de maneira permanente em discos magnéticos I BDs são muito grandes para caberem inteiramente em memória primária, com capacidade limitada de armazenamento I Custo de armazenamento em memória primária é muito alto I Memórias terciárias tem grande capacidade de armazenamento e baixo custo, mas são muito lentas e frequentemente demandam intervenção manual ( o ff -line ) I Discos magnéticos apresentam excelente relação custo-benefício, ainda mais vantajosa que outros tipos de memória secundária



## Disco Magnético (HD)

 CC BY-NC-ND 4.0 nto em Acesso aleatório Múltiplas superfícies Armazename trilhas Trilhas divididas em blocos Tamanho do bloco é fixado na formatação do HD e não pode ser trocado dinamicamente



Transferências entre memória primária e HD ocorrem em unidades de bloco



## Disco Magnético (HD)

Bloco (página) ! unidade mínima de transferência de dados entre disco e memória primária

- I Tamanho fixado na formatação, geralmente entre 512B a 8KB, que não pode ser alterado dinamicamente
- CC BY-NC-ND 4.0 I Separados nas trilhas por lacunas de tamanho fixo que incluem dados de controle, como ponteiro para o bloco subsequente I Pode ser acessado aleatoriamente pelo seu endereço de hardware, denominado endereço de bloco I Hardware controladores de disco usam o endereço do bloco para transferir o bloco do disco para um bu ff er em memória primária





## Disco Magnético (HD)



 CC BY-NC-ND 4.0 Buffer ! área reservada contígua em memória primária Memória Primária I Controladores de disco usam o endereço de bloco e de bu ff er para realizar a transferência do bloco de disco para a memória primária I Leitura (Input) ! bloco é copiado para bu ff er I Escrita (Output) ! bu ff er é copiado para bloco



## HD: Leitura e Escrita (I/O)

 beendereços CC BY-NC-ND 4.0 entar braço para 1) Controlador rece de bloco e bu ff er 2) Controlador comanda acionador a movim posicionar cabeça na trilha do endereço de bloco 3) Discos giram até o ponto de leitura e escrita 4) Dados são copiados de ou para bu ff er





## HD: Leitura e Escrita (I/O)

 CC BY-NC-ND 4.0 cessárioparaodisco Tempo de Transferência ! tempo necessário para transferir um bloco entre disco e memória primária I Tempo de Busca ! tempo necessário para posicionar a cabeça de leitura e escrita na trilha do endereço de bloco I Tempo de Latência ! ou atraso rotacional é o tempo ne girar até o ponto de leitura e escrita I Tempo de Transferência de Bloco ! tempo necessário para os dados serem copiados de ou para o bu ff er em memória primária Transferência de Bloco GLYPH&lt;28&gt; Busca + Latência 

- I Transferir múltiplos blocos consecutivos na mesma trilha ou cilindro elimina tempos de busca e latência acumulados, tornando a transferência mais eficiente



## HD: Leitura e Escrita (I/O)

Buffering de Blocos ! técnica que reserva vários bu ff ers em memória primária para agilizar a transferência de blocos do disco

- I Controladores de disco e CPUs podem operar de forma independente e paralela usando bu ff ers diferentes







## HD: Leitura e Escrita (I/O)



 CC BY-NC-ND 4.0 Duplo Buffering ! uso de dois bu ff ers para leitura ou gravação em disco I Enquanto o controlador de disco transfere dados de ou para um bu ff er , a CPU processa dados no outro bu ff er I Permite leitura ou gravação contínua em blocos consecutivos I Elimina tempos de busca e latência para todas as transferências de bloco, com exceção da primeira

- I Dados ficam prontos para processamento mais rapidamente, reduzindo ociosidade da CPU e, consequentemente o tempo de espera das aplicações



## HD: Alocação de Blocos

GLYPH&lt;1&gt;

GLYPH&lt;1&gt;

GLYPH&lt;1&gt;

 CC BY-NC-ND 4.0 A forma como os blocos são alocados em disco impacta o desempenho de I/O I Alocação Contígua ! blocos consecutivos em disco HD I Rápido I/O com duplo bu ff ering I Difícil expansão, podendo resultar em múltiplas realocações em caso de alteração dos dados



## HD: Alocação de Blocos



CC BY-NC-ND 4.0

 A forma como os blocos são alocados em disco impacta o desempenho de I/O I Alocação por Ligação ! cada bloco contém um ponteiro para o próximo I Facilita expansão I I/O mais lento pela impossibilidade de uso de duplo bu ff ering



## HD: Alocação de Blocos

A forma como os blocos são alocados em disco impacta o desempenho de I/O

- I Alocação por Segmento ! agrupa blocos consecutivos em segmentos ( clusters ) e cada segmento contém um ponteiro para o próximo segmento
- I Facilita expansão, reduzindo o número de realocações em caso de alteração dos dados



CC BY-NC-ND 4.0

 GLYPH&lt;1&gt; GLYPH&lt;1&gt; GLYPH&lt;1&gt; I Combinação de alocação contígua e por ligação I Torna duplo bu ff ering viável em um segmento, agilizando I/O



## HD: Alocação de Blocos

A forma como os blocos são alocados em disco impacta o desempenho de I/O

- I Alocação Indexada ! blocos especiais de índice são criados contendo ponteiros para blocos de dados





- I Fácil expansão, com realocações ocorrendo em blocos de índice
- CC BY-NC-ND 4.0 GLYPH&lt;15&gt; GLYPH&lt;15&gt; GLYPH&lt;1&gt; GLYPH&lt;1&gt; GLYPH&lt;1&gt; GLYPH&lt;15&gt; GLYPH&lt;1&gt; GLYPH&lt;1&gt; GLYPH&lt;1&gt; GLYPH&lt;15&gt; GLYPH&lt;15&gt; GLYPH&lt;1&gt; GLYPH&lt;1&gt; GLYPH&lt;1&gt; GLYPH&lt;15&gt; GLYPH&lt;1&gt; GLYPH&lt;1&gt; GLYPH&lt;1&gt; I Rápido I/O com busca sendo efetuada em blocos de índice, que podem ter alocação contígua ou por segmento ( duplo bu ff ering )





## Referências Bibliográficas

- [1] Elmasri, Ramez; Navathe, Sham. Fundamentals of Database Systems . 7ed. Pearson, 2016.
- [2] Silberschatz, Abraham; Korth, Henry F.; Sudarshan, S. Database System Concepts . 6ed. McGraw-Hill, 2011.
- [3] Date, Christopher J. An Introduction to Database Systems . 8ed. Pearson, 2004.





## Sistemas de Banco de Dados

Fundamentos em Bancos de Dados Relacionais



Material distribuído sob licença CC BY-NC-ND 4.0

Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International

## processamento de transação

## Transação

 CC BY-NC-ND 4.0 oumblocoúnico Conjunto de operações de acesso ao BD, constituindo uma unidade lógica I Exemplo ! saque de dinheiro em caixa eletrônico I Múltiplas operações de recuperação e atualização de dados I Todas as operações são confirmadas ou abortadas com I Somente Leitura ! somente operações de recuperação de dados I Leitura-Escrita ! contém operações de atualização de dados I Confirmada ! operações concluídas e dados registrados permanentemente I Abortada ! operações inócuas, sem qualquer efeito Tipicamente executada em sistema multiusuário de forma intercalada, em ambiente multiprogramação, ou paralela em hardware com múltiplas CPUs



## Transação

CC BY-NC-ND 4.0 comitantemente

 Processa itens de dados de forma concorrente I Item ! arquivo, bloco, registro, campo I Concorrência ! múltiplas transações concorrendo pela CPU I Maior Concorrência ! mais transações executadas con I Controle de Concorrência ! garantia de independência de execução I Granularidade ! tamanho do item de dados I Baixa (Fina) ! tamanho menor, maior concorrência, mais carga sobre o sistema de controle de concorrência I Alta (Grossa) ! tamanho maior, menor concorrência, menos carga sobre o sistema de controle de concorrência



## Transação

CC BY-NC-ND 4.0

 Executa dois tipos básicos de operação sobre itens de dados I Leitura r ( x ) ! copia item x do disco para variável de programa I Encontrar endereço de bloco de disco que contém x I Copiar bloco para bu ff er em memória primária I Copiar item x do bu ff er para variável de programa x I Escrita w x ( ) ! copia item x da variável de programa para disco I Encontrar endereço de bloco de disco que contém x I Copiar bloco para bu ff er em memória primária I Copiar item x da variável de programa x para bu ff er I Copiar bu ff er de memória para bloco de disco



## Concorrência

-  CC BY-NC-ND 4.0 Execução concorrente de múltiplas transações pode resultar em problemas I Atualização Perdida ! transações intercaladas escrevem o mesmo item, tal que a atualização de uma transação sobre o item é perdida por sobrescrição do mesmo item feita por outra transação T 1 ! r ( x ) r ( y ) x = x + y w x ( ) T 2 ! r ( x ) r ( y ) x = x GLYPH&lt;0&gt; y w x ( ) Para as transações T 1 e T 2 , considerando valores iniciais x = 10 e y = 5 I Execução sequencial ! valor final de x = 10 I Execução concorrente ! valor final de x = 5

A operação w x ( ) de T 1 foi sobrescrita por w x ( ) de T 2



## Concorrência

 CC BY-NC-ND 4.0 Execução concorrente de múltiplas transações pode resultar em problemas I Leitura Suja ! uma transação atualiza um item e falha posteriormente, sendo que nesse meio tempo, outra transação lê o item atualizado (sujo) T 1 ! r ( x ) r ( y ) x = x + y w x ( ) a T 2 ! r ( x ) r ( y ) x = x GLYPH&lt;0&gt; y w x ( ) Para as transações T 1 e T 2 , considerando valores iniciais x = 10 e y = 5: I Execução sequencial ! valor final de x = 5 I Execução concorrente ! valor final de x = 10 A operação r ( x ) de T 2 fez uma leitura suja de w x ( ) de T 1 , que falhou



## Concorrência

-  CC BY-NC-ND 4.0 Execução concorrente de múltiplas transações pode resultar em problemas I Leitura Não Repetitiva ! a mesma transação lê valores diferentes para o mesmo item em momentos diferentes, uma vez que outras transações alteraram o valor do item nesse meio tempo T 1 ! r ( x ) r ( x ) T 2 ! r ( x ) r ( y ) x = x GLYPH&lt;0&gt; y w x ( ) A primeira e a última operação r ( x ) de T 1 leem valores diferentes de x não escritos por T 1 , o que pode ocasionar um problema na lógica de processamento se um teste condicional ( x = ) x for executado, por exemplo



## Concorrência

-  CC BY-NC-ND 4.0 Execução concorrente de múltiplas transações pode resultar em problemas I Resumo Incorreto ! uma transação calcula uma função de agregação sobre itens que estão sendo atualizados por outras transações, provendo valores de resumo incorretos Técnicas de controle de concorrência resolvem os problemas, garantindo execução concorrente e independente de transações I Bloqueio ! técnica baseada em bloqueios de leitura e escrita em itens I Restringe a concorrência I Transações bloqueiam e desbloqueiam itens quando necessário I Sujeito a problemas de travamento ( deadlock ) e espera indefinida ( starvation )



## Falha

CC BY-NC-ND 4.0

 Execução concorrente de transações está sujeita a diferentes tipos de falhas I Sistema ! hardware, software ou rede I Operação ! interrupção do usuário, lógica de programação I Concorrência ! técnica de controle de concorrência I Condição de Exceção ! programada na própria transação I Disco ! blocos de dados perdidos I Catástrofe ! blackout , incêndio, roubo, formatação acidental de disco Sistemas de banco de dados estão preparados para lidar com falhas I Logging ! registro histórico de transações I Dumping ! cópia de segurança do banco de dados



## Processamento de Transações

 CC BY-NC-ND 4.0 Adicionalmente às operações de leitura e escrita sobre itens de dados, existem operações necessárias ao processamento de transações I Begin Transaction ( b ) ! marca o início da transação I End Transaction ( e ) ! marca o fim da transação I Commit ( c ) ! marca o ponto de confirmação de operações I Abort ( a ) ! ou rollback , marca o ponto de anulação de operações Uma transação só é considerada terminada quando falhar, ou todas as suas operações tiverem sido executadas e registradas do arquivo de log do sistema Início





## Processamento de Transações

 CC BY-NC-ND 4.0 vemcontinuar Transações possuem propriedades que devem ser mantidas no processamento I A tomicidade ! unidade atômica, executada integralmente ou não executada de forma alguma I C onsistência ! restrições especificadas no esquema de sendo respeitadas após processamento I I solamento ! independência de execução, sem sofrer interferência de transações concorrentes I Nível 0 ! sem leitura suja I Nível 1 ! sem atualização perdida I Nível 2 ! níveis 0 + 1 I Nível 3 ! nível 2, com leitura repetitiva

- I D urabilidade ! alterações confirmadas devem persistir



## Processamento de Transações

 CC BY-NC-ND 4.0 Escalonamento (Schedule) ! intercalação de operações de transações distintas para execução simultânea Sa ! b 1 ; r 1 ( x ) ; b 2 ; r 2 ( x ) ; r 1 ( y ) ; w 2 ( x ) ; w 1 ( y ) ; c 2 ; e 2 ; a 1 ; e 1 I Sa ! escalonamento a I oi ! operação o 2 f a b c e r w ; ; ; ; ; g realizada pela transação i I x y ; ! itens de dados lidos ou escritos pelas transações I Tipicamente b e e não são representadas, presumindo que b ocorre logo antes da primeira operação da transação, e e logo depois da última Sa ! r 1 ( x ) ; r 2 ( x ) ; r 1 ( y ) ; w 2 ( x ) ; w 1 ( y ) ; c 2 ; a 1



## Escalonamento de Transações

Operações em um escalonamento podem estar em situação de conflito

- I Pertencem a transações diferentes
- I Operam sobre o mesmo item
- I Ao menos uma delas é w

CC BY-NC-ND 4.0

 Sa ! r 1 ( x ) ; r 2 ( x ) ; r 1 ( y ) ; w 2 ( x ) ; w 1 ( y ) ; c 2 ; a 1



## Escalonamento de Transações

 Completo ! possui todas as operações de cada transação I Operações são exatamente as mesmas das transações originais I A ordem das operações nas transações originais é preservada I Operações em conflito precedem ou sucedem umas as I Exemplo ! para as transações T 1 e T 2 T 1 ! r ( x ) ; r ( y ) ; w y ( ) ; a T 2 ! r ( x ) ; w x ( ) ; c o escalonamento Sa é completo Sa ! r 1 ( x ) ; r 2 ( x ) ; r 1 ( y ) ; w 2 ( x ) ; w 1 ( y ) ; c 2 ; a 1

CC BY-NC-ND 4.0 outras

Improváveis, novas transações são incorporadas a escalonamentos existentes



## Escalonamento de Transações

 CC BY-NC-ND 4.0 Recuperável ! transação confirmada não será desfeita, garantindo durabilidade I Leitura Suja ! pode demandar reversão de confirmação Sa ! r 1 ( x ) ; r 2 ( x ) ; w 1 ( x ) ; r 1 ( y ) ; w 2 ( x ) ; r 1 ( x ) ; c 1 ; c 2 I Nenhuma transação T que leia um item escrito por outra transação T 0 pode confirmar antes de T 0 Sa ! r 1 ( x ) ; r 2 ( x ) ; w 1 ( x ) ; r 1 ( y ) ; w 2 ( x ) ; r 1 ( x ) ; c 2 ; c 1



## Escalonamento de Transações

CC BY-NC-ND 4.0 tra

 Serial ! sem intercalação, com todas as operações de uma transação precedendo todas as operações de outra Sa ! r 1 ( x ) ; w 1 ( x ) ; r 1 ( y ) ; r 1 ( x ) ; c 1 ; r 2 ( x ) ; w 2 ( x ) ; c 2 I Isolamento ! transação não sofre interferência de ou I Concorrência ! limitada, gerando ociosidade de CPU Não Serial ! operações de transações intercaladas Sa ! r 1 ( x ) ; r 2 ( x ) ; w 1 ( x ) ; r 1 ( y ) ; w 2 ( x ) ; r 1 ( x ) ; c 2 ; c 1 I Isolamento ! não é garantido

- I Concorrência ! melhor aproveitamento de CPU



## Escalonamento de Transações

CC BY-NC-ND 4.0

 Serialização ! processo de determinação de escalonamentos não seriais que sejam equivalentes a seriais, garantindo isolamento I Multiplicidade ! n ! escalonamento seriais possíveis para n transações, e um número muito maior de escalonamentos não seriais possíveis I Serializável ! não serial equivalente a um serial I Não Serializável ! não equivalente a qualquer serial I Escalonamentos serializáveis são corretos I Equivalência ! operações são aplicadas a itens na mesma ordem I Conflito ! ordem de operações em conflito nos escalonamentos é a mesma I Visão ! operações r tem a mesma visão de itens nos escalonamentos



## Escalonamento de Transações

-  CC BY-NC-ND 4.0 Equivalência por Conflito ! mesma ordem de operações em conflito Sa ! r 1 ( x ) ; w 1 ( x ) ; r 1 ( y ) ; w 1 ( y ) ; r 2 ( x ) ; w 2 ( x ) Sb ! r 2 ( x ) ; w 2 ( x ) ; r 1 ( x ) ; w 1 ( x ) ; r 1 ( y ) ; w 1 ( y ) Sc ! r 1 ( x ) ; r 2 ( x ) ; w 1 ( x ) ; r 1 ( y ) ; w 2 ( x ) ; w 1 ( y ) Sd ! r 1 ( x ) ; w 1 ( x ) ; r 2 ( x ) ; w 2 ( x ) ; r 1 ( y ) ; w 1 ( y ) I Sd é serializável, enquanto Sc não é I Sc não equivalente a Sa ! ordem w 1 ( x ) e r 2 ( x ) diferente I Sc não equivalente a Sb ! ordem w 2 ( x ) e r 1 ( x ) diferente I Sd equivalente a Sa ! mesma ordem para operações em conflito



## Escalonamento de Transações

CC BY-NC-ND 4.0

 seriais Grafo de Precedência ! permite verificar se escalonamento é serializável sem precisar checar equivalência por conflito com n ! escalonamentos I Direcionado ! ausência de ciclos indica escalonamento serializável I Nós ! transações do escalonamento I Arestas ! conflitos entre operações de transações I De transação sucedente para precedente, com operações em conflito Sc ! r 1 ( x ) ; r 2 ( x ) ; w 1 ( x ) ; r 1 ( y ) ; w 2 ( x ) ; w 1 ( y )





## Processamento de Transações

CC BY-NC-ND 4.0

 SGBDs tipicamente permitem configuração de características de processamento de transações através do comando set transaction I Acesso ! operações permitidas em transações I rw ! leitura e escrita (modo padrão) I ro ! somente leitura I Área de Diagnóstico ! últimas n instruções SQL executadas I Isolamento ! nível de isolamento requerido no processamento I read uncommited !: atualização perdida I read commited !: (atualização perdida \_ leitura suja) I repeatable read !: (atualização perdida \_ leitura suja) ^ leitura repetitiva

- I serializable !: (atualização perdida \_ leitura suja \_ resumo incorreto) ^ leitura repetitiva



## Referências Bibliográficas

- [1] Elmasri, Ramez; Navathe, Sham. Fundamentals of Database Systems . 7ed. Pearson, 2016.
- [2] Silberschatz, Abraham; Korth, Henry F.; Sudarshan, S. Database System Concepts . 6ed. McGraw-Hill, 2011.
- [3] Date, Christopher J. An Introduction to Database Systems . 8ed. Pearson, 2004.



## Sistemas de Banco de Dados

Fundamentos em Bancos de Dados Relacionais



Material distribuído sob licença CC BY-NC-ND 4.0

Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International

## sql: definição de dados





 CC BY-NC-ND 4.0 recomoexecutara S tructured Q uery L anguage I Linguagem de consulta estruturada I Linguagem declarativa de alto nível I Usuário especifica o que deseja, deixando decisões sob consulta para o SGBD I Contém instruções para definição e manipulação de dados I Padrão em SGBDs relacionais comerciais I Mantém equivalência com o modelo relacional I Relação ! Tabela I Tupla ! Linha

- I Atributo ! Coluna



## SQL: Recursos

 SQL oferece múltiplos recursos I Definição de visões sobre dados I Definição de restrições sobre os dados I Especificação de controles de transações I Especificação de autorizações e segurança

CC BY-NC-ND 4.0





## SQL: Definição de Dados

 Existem diferentes instruções (comandos) para definição de dados I CREATE ! cria elementos no catálogo, como esquemas tabelas , e domínios I ALTER ! modifica elementos no catálogo I DROP ! remove elementos do catálogo

CC BY-NC-ND 4.0





## SQL: Definição de Dados

CC BY-NC-ND 4.0 a

 Esquema ! elemento que agrupa outros elementos que pertencem à mesma aplicação de BD I Nome ! identificador do esquema I Proprietário ! usuário com autoridade sobre o esquem Exemplo ! criar esquema UNIVERSIDADE pertencente ao usuário 'Pedro' CREATE SCHEMA UNIVERSIDADE AUTHORIZATION 'Pedro';



## SQL: Definição de Dados

 Catálogo ! coleção nomeada de esquemas I Contém o esquema padrão que oferece informação sobre todos os esquemas no catálogo, bem como sobre os descritores dos elementos I Esquema padrão ! INFORMATION\_SCHEMA Tabela Base ! declarada por meio da instrução CREATE TABLE I Tabela realmente criada e armazenada como um arquivo pelo SGBD Tabela Virtual ! declarada por meio da instrução CREATE VIEW

- I Tabela pode ser criada e armazenada como um arquivo pelo SGBD
- I Geralmente não são realmente armazenados em arquivo

CC BY-NC-ND 4.0





## SQL: Definição de Dados

 ascolunase CC BY-NC-ND 4.0 tiposãocriadas, CREATE TABLE I Cria uma nova tabela, dando-lhe um nome e especificando su restrições iniciais I Restrições de tipo são geralmente especificadas I Uma vez que colunas e suas respectivas restrições de podem ser redefinidas a partir da instrução ALTER TABLE Exemplo: CREATE TABLE PROFESSOR;

Esquema em que as tabelas são criadas é especificado implicitamente no ambiente em que as instruções CREATE TABLE são executadas



## SQL: Restrições

 CC BY-NC-ND 4.0 Restrições podem ser especificadas em SQL como parte da criação de tabela I Tipo ! domínio de valores válidos para a coluna I Nulidade ! possibilidade de valor NULL em coluna I Valor ! faixa de valores válidas para uma coluna I Valor Padrão ! valor atribuído a uma coluna caso nenhum valor seja especificado I Chave ! coluna(s) identificadora(s) de uma instância I Unicidade ! coluna(s) candidata(s) a identificadora(s) de uma instância I Integridade Referencial ! regras para atualização de linhas correlacionadas em diferentes tabelas



## SQL: Restrição de Tipo

 EALeDOUBLE CC BY-NC-ND 4.0 diferentestipos Numérico ! incluem números inteiros de vários tamanhos (INTEGER e SMALLINT) e números de ponto flutuante (reais) de várias posições (FLOAT, R PRECISION) Cadeias de Caracteres ! incluem cadeias de caracteres de I CHAR( n ) ! cadeias de tamanho fixo, onde n é a quantidade exata de caracteres a ser armazenada I VARCHAR( n ) ! cadeias de tamanho variável, onde n é a quantidade máxima de caracteres armazenados I Valor literal da cadeia de caracteres deve ser especificado entre aspas simples, com maiúsculas diferenciadas de minúsculas ( case sensitive )



## SQL: Restrição de Tipo

 CC BY-NC-ND 4.0 éaquantidade Cadeias de Bits ! incluem cadeias binárias de diferentes tipos I BIT( n ) ! cadeias de tamanho fixo, onde n é a quantidade exata de bits a ser armazenada I BIT VARYING( n ) ! cadeias de tamanho variável, onde n máxima de bits armazenados I Ovalor literal da cadeia de bits deve ser especificado entre apóstrofos, precedidos por um B para distingui-los das cadeias de caracteres I Exemplo ! B'10101' Booleano ! valores binários verdadeiro (1) e falso (0)





## SQL: Restrição de Tipo

-  CC BY-NC-ND 4.0 Date &amp; Time ! valores de data e hora I Date ! dez posições compostas de dia, mês e ano na forma DD-MM-YYYY I Time ! oito posições compostas de hora, minuto e segundo na forma HH:MM:SS Timestamp ! valores temporais de alta precisão I Inclui os campos DATE e TIME, mais um mínimo de seis posições para frações decimais de segundos e um qualificador opcional WITH TIME ZONE I Valores literais representados por cadeias entre apóstrofos precedidos pela palavra-chave TIMESTAMP na forma TIMESTAMP '27-09-2008 09:12:47.648302'



## SQL: Restrição de Nulidade

);

CC BY-NC-ND 4.0

 Pode ser especificada se valor NULL não for permitido para determinada coluna I Implícito para colunas que fazem parte da chave primária Exemplo: CREATE TABLE PROFESSOR ( CPF CHAR(11) NOT NULL, Nome VARCHAR(80) NOT NULL, Departamento INT



## SQL: Restrição de Valor Padrão

## Define valor padrão para uma coluna

- I Valor padrão será incluído em qualquer nova linha se um valor explícito não for fornecido para essa coluna

## Exemplo:



- CC BY-NC-ND 4.0 áNULLparacolunas I Se essa restrição não for especificada valor padrão ser que não possuem a restrição NOT NUL. CREATE TABLE PROFESSOR ( CPF CHAR(11) NOT NULL, Nome VARCHAR(80) NOT NULL, Departamento INT DEFAULT 1

);



## SQL: Restrição de Valor

 CC BY-NC-ND 4.0 Limita valores possíveis para coluna Exemplo ! supondo que números de departamento sejam restritos a inteiros entre 1 e 20, podemos modificar a tabela professor , adicionando uma restrição para a coluna Departamento : ALTER TABLE PROFESSOR ADD CHECK (Departamento &gt; 0 AND Departamento &lt; 21);



## SQL: Restrição de Chave

Especifica uma ou mais colunas que compõem a chave primária de uma tabela

## Exemplo:

 CC BY-NC-ND 4.0 I Se a chave primária for composta por apenas uma coluna, a cláusula PRIMARY KEY pode acompanhar a coluna diretamente CREATE TABLE PROFESSOR ( CPF CHAR(11) NOT NULL, Nome VARCHAR(80) NOT NULL, Departamento INT, PRIMARY KEY (CPF) );



## SQL: Restrição de Unicidade

-  CC BY-NC-ND 4.0 Especifica chaves secundárias alternativas I Pode ser especificada diretamente para chave secundária em coluna única Exemplo: CREATE TABLE PROFESSOR ( CPF CHAR(11) NOT NULL, Nome VARCHAR(80) NOT NULL, Departamento INT, PRIMARY KEY (CPF), UNIQUE (Nome) );



## SQL: Restrição de Integridade Referencial

 veestrangeira CC BY-NC-ND 4.0 Estabelece regras para restrição de atualização de linhas correlacionadas em diferentes tabelas através de referência à chave primária por cha Exemplo: CREATE TABLE PROFESSOR ( CPF CHAR(11) NOT NULL, Nome VARCHAR(80) NOT NULL, Departamento INT, PRIMARY KEY (CPF), FOREIGN KEY (Departamento) REFERENCES DEPARTAMENTO(Numero) );



## SQL: Restrição de Integridade Referencial

 olinhassão CC BY-NC-ND 4.0 I A integridade referencial entre tabelas pode ser violada quand manipuladas ou o valor de uma chave primária é modificado I Ação de disparo referencial especifica uma ação alternativa para os casos de violação de integridade: I RESTRICT ! a linha da chave primária não pode ser modificada se houver linhas contendo chaves estrangeiras associadas a ela I CASCADE ! a linha da chave primária, bem como as linhas contendo chaves estrangeiras são modificadas I SET NULL ! a linha da chave primária é modificada, desde que se consiga atualizar para NULL as chaves estrangeiras associadas a ela

- I SET DEFAULT ! a linha da chave primária é modificada, desde que as chaves estrangeiras associadas a ela possuam valor padrão que possa ser usado



## SQL: Restrição de Integridade Referencial

Exemplo:

CC BY-NC-ND 4.0

(

CPF

CHAR(11)

NOT

NULL,

Nome

Departamento

INT

DEFAULT

1,

PRIMARY

KEY

(CPF),

FOREIGN

KEY

(Departamento)

REFERENCES

DEPARTAMENTO(Numero)

);

 Ações de disparo devem ser escolhidas em caso de remoção ( ON DELETE ) ou atualização ( ON UPDATE ) CREATE TABLE PROFESSOR VARCHAR(80) NOT NULL, ON DELETE SET DEFAULT ON UPDATE CASCADE



## SQL: Restrições Nomeadas

-  CC BY-NC-ND 4.0 Restrição pode ser rotulada utilizando o descritor CONSTRAINT I Nomes de todas as restrições de um esquema precisam ser exclusivos Exemplos: CONSTRAINT PK\_PROFESSOR PRIMARY KEY (CPF); CONSTRAINT FK\_DEPARTAMENTO\_PROFESSOR FOREIGN KEY (Departamento) REFERENCES DEPARTAMENTO(Numero) ON DELETE SET DEFAULT ON UPDATE CASCADE;



## Referências Bibliográficas

- [1] Elmasri, Ramez; Navathe, Sham. Fundamentals of Database Systems . 7ed. Pearson, 2016.
- [2] Silberschatz, Abraham; Korth, Henry F.; Sudarshan, S. Database System Concepts . 6ed. McGraw-Hill, 2011.
- [3] Date, Christopher J. An Introduction to Database Systems . 8ed. Pearson, 2004.



## Sistemas de Banco de Dados

Fundamentos em Bancos de Dados Relacionais



Material distribuído sob licença CC BY-NC-ND 4.0

Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International

## modelo relacional



## Modelo Relacional

 Modelo de implementação (representativo) baseado no paradigma relacional I Dados são organizados de maneira tabular: I Entidade ! Relação I Relacionamento ! Relacionamento I Atributo ! Atributo I Registro ! Tupla I Pode ser criado a partir do EER utilizando um procedimento em 7 etapas

CC BY-NC-ND 4.0





## Diagrama EER: Sistema de Matrícula





## Mapeamento EER

 CC BY-NC-ND 4.0 Etapa 1 ! Entidades Fortes I Crie uma relação para cada entidade forte e inclua todos os atributos simples I Inclua apenas atributos simples de um atributo composto I Escolha um dos atributos chave da entidade forte como chave primária da nova relação I Se a chave escolhida for composta, o conjunto de atributos simples que a compõe formarão a chave primária



## Mapeamento EER

## Etapa 1 ! Entidades Fortes





## Mapeamento EER

## Etapa 2 ! Entidades Fracas

- I Crie uma relação para cada entidade fraca e inclua todos os atributos simples
- CC BY-NC-ND 4.0 osatributosde I Inclua como atributos de chave estrangeira da relação, chave primária da relação que corresponde à entidade proprietária I Escolha a chave estrangeira e um atributo chave parcial como chave primária da nova relação





## Mapeamento EER

Etapa 2 ! Entidades Fracas





## Mapeamento EER

## Etapa 3 ! Relacionamentos Binários 1:N

- I Identifique a relação R 1 que representa a entidade participante no lado N do relacionamento
- CC BY-NC-ND 4.0 de 2,que I Inclua como chave estrangeira em R 1 a chave primária R representa a outra entidade participante do relacionamento





## Mapeamento EER

## Etapa 3 ! Relacionamentos Binários 1:N

 CC BY-NC-ND 4.0 CURSO Sigla Nome Horas Custo Area AREA Sigla Nome SuperArea MODULO Sigla Nome Curso TOPICO Modulo Sigla Nome Horas ALUNO CPF Nome Sobrenome Sexo

DataNasc



## Mapeamento EER

 CC BY-NC-ND 4.0 cionamento Etapa 4 ! Relacionamentos Binários N:N I Crie uma nova relação R 3 para cada relacionamento N:N I Inclua como chave estrangeira em R 3 as chaves primárias das relações R 1 e R 2, que representam as entidades participantes no rela I A chave primária de R 3 será formada pela combinação das chaves estrangeiras em R 3



## Mapeamento EER

## Etapa 4 ! Relacionamentos Binários N:N

 CC BY-NC-ND 4.0 CURSO Sigla Nome Horas Custo Area AREA Sigla Nome SuperArea MODULO Sigla Nome Curso TOPICO Modulo Sigla Nome Horas MATRICULA Curso Aluno Data Pago ALUNO CPF Nome Sobrenome Sexo

DataNasc



## Mapeamento EER

## Etapa 5 ! Relacionamentos Binários 1:1

- I Identifique as relações que correspondem às entidades participantes
- I Existem três estratégias:
- CC BY-NC-ND 4.0 1. Mesclagem ! consiste em mesclar as entidades e o relacionamento em uma única relação 2. Chave Estrangeira ! consiste em mapear o relacionamento 1:1 como um relacionamento 1:N 3. Referência Cruzada ! consiste em mapear o relacionamento 1:1 como um relacionamento N:N





## Mapeamento EER

-  CC BY-NC-ND 4.0 toquetenhaAcomo Etapa 6 ! Atributos Multivalorados I Crie uma nova relação para cada atributo multivalorado A I A nova relação incluirá um atributo de A, mais o atributo da chave primária da relação que representa a entidade ou relacionamen atributo multivalorado



## Mapeamento EER

## Etapa 6 ! Atributos Multivalorados

DataNasc





## Mapeamento EER

## Etapa 7 ! Relacionamentos de Alto Grau

- I Crie uma relação R 3 para cada relacionamento n -ário, em que n &gt; 2
- I Inclua como chave estrangeira em R 3 as chaves primárias das relações que representam as entidades participantes
- CC BY-NC-ND 4.0 I A chave primária de R 3 é a combinação de todas as chaves estrangeiras que referenciam as relações das entidades participantes





## Modelo Relacional: Sistema de Matrícula





## Referências Bibliográficas

- [1] Elmasri, Ramez; Navathe, Sham. Fundamentals of Database Systems . 7ed. Pearson, 2016.
- [2] Silberschatz, Abraham; Korth, Henry F.; Sudarshan, S. Database System Concepts . 6ed. McGraw-Hill, 2011.
- [3] Date, Christopher J. An Introduction to Database Systems . 8ed. Pearson, 2004.



## Sistemas de Banco de Dados

Fundamentos em Bancos de Dados Relacionais



Material distribuído sob licença CC BY-NC-ND 4.0

Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International

## sql: manipulação de dados





 CC BY-NC-ND 4.0 recomoexecutara S tructured Q uery L anguage I Linguagem de consulta estruturada I Linguagem declarativa de alto nível I Usuário especifica o que deseja, deixando decisões sob consulta para o SGBD I Contém instruções para definição e manipulação de dados I Padrão em SGBDs relacionais comerciais I Mantém equivalência com o modelo relacional I Relação ! Tabela I Tupla ! Linha

- I Atributo ! Coluna



## SQL: Manipulação de Dados

 Existem diferentes instruções (comandos) para manipulação de dados I INSERT ! inserir linhas em tabelas I DELETE ! remover linhas de tabelas I UPDATE ! atualizar valores de colunas em linhas de t I SELECT ! recuperar dados em tabelas

CC BY-NC-ND 4.0 abelas 



## Instrução INSERT

 CC BY-NC-ND 4.0 Acrescenta uma linha em uma tabela I Necessário especificar o nome da tabela e uma lista de valores para a linha I Valores devem ser listados na mesma ordem em que as colunas correspondentes foram definidas na tabela PROFESSOR CPF Nome Sexo Salario Departamento INSERT INTO PROFESSOR VALUES ('12345678900', 'Ricardo Marini', 'M', 3000.00, 1);



## Instrução INSERT

 CC BY-NC-ND 4.0 É possível especificar nomes de colunas correspondentes a valores fornecidos PROFESSOR CPF Nome Sexo Salario Departamento INSERT INTO PROFESSOR (CPF, Sexo, Nome, Departamento) VALUES ('12345678900', 'M', 'Ricardo Marini', 1); Coluna não especificada tem seu valor definido como DEFAULT ou NULL, sendo que valores e colunas devem ser listadas na mesma ordem



## Instrução INSERT

|         CPF | Nome                      | Sexo   |   Salario | Departamento   |
|-------------|---------------------------|--------|-----------|----------------|
| 12345678900 | Roberto Machado           | M      |      1200 | 1              |
| 12345678901 | Manuela Costa             | F      |      2700 | 4.0 3          |
| 21345678900 | Carlos A. Martins         | M      |      3200 | 1              |
| 32145678900 | Cardoso Ana Maria Freitas | F      |      7500 | 2              |

Caso não exista tupla na tabela departamento com chave primária Numero = 4 para manter integridade referencial com a coluna Departamento da tabela professor a operação será rejeitada

 CC BY-NC-ND 4.0 Se alguma restrição for violada a operação é rejeitada PROFESSOR 12345678901 21345678900 32145678900 INSERT INTO PROFESSOR (CPF, Nome, Sexo, Departamento) VALUES ('68345618900', 'Amanda Ramirez', 'F', 4);



## Instrução INSERT

|         CPF | Nome                      | Sexo   |   Salario | Departamento   |
|-------------|---------------------------|--------|-----------|----------------|
| 12345678900 | Roberto Machado           | M      |      1200 | 1              |
| 12345678901 | Manuela Costa             | F      |      2700 | 4.0 3          |
| 21345678900 | Carlos A. Martins         | M      |      3200 | 1              |
| 32145678900 | Cardoso Ana Maria Freitas | F      |      7500 | 2              |

Valor da chave primária CPF não foi fornecido, o que viola a restrição de chave, logo a operação será rejeitada

 CC BY-NC-ND 4.0 Se alguma restrição for violada a operação é rejeitada PROFESSOR 12345678901 21345678900 32145678900 INSERT INTO PROFESSOR (Nome, Sexo, Departamento) VALUES ('Amanda Ramirez', 'F', 1);



## Instrução INSERT

 CC BY-NC-ND 4.0 É possível inserir múltiplas linhas na tabela usando a instrução INSERT combinada com a instrução SELECT INSERT INTO PROFESSOR (CPF, Nome, Sexo, Departamento) SELECT CPF, Nome, Sexo, 1 FROM ALUNO; Nesse caso, todas as linhas da tabela aluno serão inseridas na tabela professor , sendo que para todas as linhas inseridas a coluna Departamento terá valor 1



## Instrução DELETE

 CC BY-NC-ND 4.0 Remove linhas de uma tabela I Linhas são excluídas de apenas uma tabela I Exceção ! exclusão pode se propagar para linhas em outras tabelas, de acordo com restrições de integridade referencial I Condição (cláusula WHERE) inexistente especifica que todas as linhas na tabela serão excluídas I Tabela permanece no BD como uma tabela vazia



## Instrução DELETE

Exemplo:

|         CPF | Nome                      | Sexo   |   Salario | Departamento   |
|-------------|---------------------------|--------|-----------|----------------|
| 12345678900 | Roberto Machado           | M      |      1200 | 1              |
| 12345678901 | Manuela Costa             | F      |      2700 | 4.0 3          |
| 21345678900 | Carlos A. Martins         | M      |      3200 | 1              |
| 32145678900 | Cardoso Ana Maria Freitas | F      |      7500 | 2              |

DELETE FROM PROFESSOR WHERE Salario &lt; 1000,00;

Instrução não removerá nenhuma linha da tabela

 PROFESSOR

CC BY-NC-ND 4.0



## Instrução DELETE

## Exemplo:

|         CPF | Nome                      | Sexo   |   Salario | Departamento   |
|-------------|---------------------------|--------|-----------|----------------|
| 12345678900 | Roberto Machado           | M      |      1200 | 1              |
| 12345678901 | Manuela Costa             | F      |      2700 | 4.0 3          |
| 21345678900 | Carlos A. Martins         | M      |      3200 | 1              |
| 32145678900 | Cardoso Ana Maria Freitas | F      |      7500 | 2              |

DELETE FROM PROFESSOR WHERE Sexo = 'M';

Instrução removerá duas linha da tabela

 PROFESSOR

CC BY-NC-ND 4.0



## Instrução DELETE

## Exemplo:

|         CPF | Nome                      | Sexo   |   Salario | Departamento   |
|-------------|---------------------------|--------|-----------|----------------|
| 12345678900 | Roberto Machado           | M      |      1200 | 1              |
| 12345678901 | Manuela Costa             | F      |      2700 | 4.0 3          |
| 21345678900 | Carlos A. Martins         | M      |      3200 | 1              |
| 32145678900 | Cardoso Ana Maria Freitas | F      |      7500 | 2              |

DELETE FROM PROFESSOR;

Instrução removerá todas as linha da tabela

 PROFESSOR

CC BY-NC-ND 4.0



## Instrução UPDATE

-  CC BY-NC-ND 4.0 lasdeacordocom Modifica valores em colunas de uma ou mais linhas I Cada instrução afeta apenas uma tabela I Exceção ! atualização de uma chave primária pode ser propagada para os valores de chave estrangeira das linhas em outras tabe restrições de integridade referencial I Cláusula SET especifica colunas a serem modificadas e seus novos valores



## Instrução UPDATE

CC BY-NC-ND 4.0

 Exemplos: UPDATE PROFESSOR SET Salario = 2500,00, Departamento = 2 WHERE CPF = '12345678900'; Altera o salário e o número do departamento do professor de determinado CPF UPDATE PROFESSOR SET Salario = Salario * 1.1; Aumenta em 10% o salário de todos os professores



## Instrução SELECT

- I &lt;condição&gt; ! expressão condicional que identifica linhas que devem ser recuperadas pela consulta

 hamadode CC BY-NC-ND 4.0 Recupera linhas em múltiplas tabelas I Mapeamento ! forma básica da instrução SELECT, também c bloco select-from-where SELECT &lt;lista de colunas&gt; FROM &lt;lista de tabelas&gt; WHERE &lt;condição&gt;; I &lt;lista de colunas&gt; ! lista de nomes de colunas que valores devem ser recuperados pela consulta I &lt;lista de tabelas&gt; ! lista dos nomes de tabelas necessárias para processar a consulta



## Instrução SELECT

Exemplo ! recuperar o nome e o salário de todos os professores do sexo masculino do departamento de número 1

|         CPF | Nome                    | Sexo   |   Salario | Departamento   |
|-------------|-------------------------|--------|-----------|----------------|
| 12345678900 | Cardoso Roberto Machado | M      |      1200 | 1              |
| 12345678901 | Manuela Costa           | F      |      2700 | 4.0 3          |
| 21345678900 | Carlos A. Martins       | M      |      3200 | 1              |
| 32145678900 | Ana Maria Freitas       | F      |      7500 | 2              |

SELECT

FROM

WHERE

1

AND

Sexo = 'M';

CC BY-NC-ND 4.0

 PROFESSOR Nome, Salario PROFESSOR Departamento =



## Instrução SELECT

Exemplo ! recuperar o CPF e o nome dos professores do sexo masculino que também são alunos

SELECT

FROM

WHERE

AND

Resultado:

 CC BY-NC-ND 4.0 A.CPF, A.Nome PROFESSOR A, ALUNO B A.CPF = B.CPF A.Sexo = 'M'; CPF Nome 12345678900 Roberto Machado 21345678900 Carlos A. Martins

|         CPF | Nome              |
|-------------|-------------------|
| 12345678900 | Roberto Machado   |
| 21345678900 | Carlos A. Martins |



## Instrução SELECT

Exemplo ! recuperar o nome do departamento e do professor para todos os professores que são alunos e que trabalham no departamento de Pesquisa

SELECT

FROM

WHERE

AND

AND

A.Nome

=

Resultado:

 nome CC BY-NC-ND 4.0 A.Nome AS Departamento, B.Nome AS Professor DEPARTAMENTO A, PROFESSOR B, ALUNO C A.Numero = B.Departamento B.CPF = C.CPF 'Pesquisa'; Departamento Professor Pesquisa Roberto Machado

Pesquisa

Carlos A. Martins



## Instrução SELECT

CC BY-NC-ND 4.0

Junções podem ser especificadas tanto na cláusula WHERE quanto na cláusula FROM com o uso do operador JOIN

SELECT

FROM

WHERE

AND

SELECT

FROM

WHERE

 A.CPF, A.Nome PROFESSOR A, ALUNO B A.CPF = B.CPF A.Sexo = 'M'; A.CPF, A.Nome PROFESSOR A JOIN ALUNO B ON A.CPF = B.CPF A.Sexo = 'M';

Variações do operador de junção podem ser especificados, como INNER JOIN , LEFT OUTER JOIN e FULL JOIN



## Ambiguidade

CC BY-NC-ND 4.0

 paraevitar Mesmo nome pode ser usado em mais de uma coluna, desde que as colunas pertençam a tabelas diferentes e estejam devidamente prefixadas ambiguidade SELECT PROFESSOR.Nome, ALUNO.Nome FROM PROFESSOR, ALUNO WHERE PROFESSOR.CPF = ALUNO.CPF AND PROFESSOR.Sexo = 'M'; SELECT A.Nome, B.Nome FROM PROFESSOR A, ALUNO B WHERE A.CPF = B.CPF AND A.Sexo = 'M';



## Ausência de Cláusula WHERE

-  CC BY-NC-ND 4.0 Inexistência de condições para seleção e junção de linhas traz impactos diferentes no resultado das consultas I Tabela Única ! todas as linhas da única tabela especificada na cláusula FROM são retornadas SELECT CPF FROM PROFESSOR; I Múltiplas Tabelas ! todas as combinações possíveis entre linhas das tabelas especificadas na cláusula FROM são retornadas, equivalendo à operação Produto Cartesiano da álgebra relacional SELECT A.CPF

FROM

PROFESSOR A, DEPARTAMENTO B;



## Duplicatas

WHERE

Salario &lt; 5000.00;



|   4.0 Departamento |
|--------------------|
|                  1 |
|                  3 |
|                  1 |



 CC BY-NC-ND 4.0 nto Uma tabela constitui um multiconjunto e linhas duplicadas podem aparecer no resultado de uma consulta I DISTINCT ! elimina linhas duplicadas no resultado SELECT Departamento FROM PROFESSOR WHERE Salario &lt; 5000.00; SELECT DISTINCT Departamento FROM PROFESSOR Departamento



## Operadores Especiais

 CC BY-NC-ND 4.0 Asterisco (*) ! recupera todas as colunas das linhas selecionadas sem a necessidade de listar seus nomes explicitamente SELECT * FROM PROFESSOR WHERE Departamento = 1 Nesse caso, recupera todas as colunas de professores que trabalham no departamento de número 1





## Operadores Especiais

 CC BY-NC-ND 4.0 LIKE ! comparação sobre subcadeias de caracteres I Subcadeias são especificadas usando dois caracteres especiais I % substitui zero ou mais caracteres I \_ substitui um único caracter SELECT CPF, Nome FROM PROFESSOR WHERE Endereco LIKE '%Belo Horizonte%'; Recupera o CPF e nome de todos os professores em que seu endereço contenha a subcadeia de caracteres Belo Horizonte



## Operadores Especiais

CC BY-NC-ND 4.0

 BETWEEN ! comparação com intervalos I Valores para colunas comparadas devem estar entre um intervalo de valores SELECT * FROM PROFESSOR WHERE Salario BETWEEN 2000,00 AND 5000,00; Recupera todas as colunas de professores com salários entre 2 e 5 mil



## Ordenação de Resultados

 CC BY-NC-ND 4.0 ORDER BY ! ordena linhas do resultado de uma consulta I ASC ! operador padrão para ordenação crescente I DESC ! operador para ordenação decrescente SELECT A.Nome, B.Nome FROM DEPARTAMENTO A, PROFESSOR B WHERE A.Numero = B.Departamento ORDER BY B.Nome, A.nome DESC; Recupera o nome do departamento e do professor para todos os professores que trabalham em um departamento, ordenando o resultado de maneira crescente pelo nome do professor e decrescente pelo nome do departamento



## Valores NULL

Recupera o CPF e o nome dos professores que não trabalham em algum departamento

CC BY-NC-ND 4.0

 IS NULL ( IS NOT NULL ) ! verifica se valor de coluna é NULL I NULL tem semântica imprecisa I Valor desconhecido? I Valor indisponível? I Valor não aplicável? SELECT CPF, Nome FROM PROFESSOR WHERE Departamento IS NULL;



## Consulta Aninhada

Recupera nome e salário dos professores que possuem mesmo CPF e nome de algum aluno, desde que tenham o mesmo sexo

CC BY-NC-ND 4.0

 Bloco SELECT completo na cláusula WHERE de outra consulta, denominada consulta externa I IN ( NOT IN ) ! verifica se um conjunto de valores pertence a um multiconjunto de valores SELECT A.Nome, A.Salario FROM PROFESSOR A WHERE (A.CPF, A.Nome) IN (SELECT B.CPF, B.Nome FROM ALUNO B WHERE A.Sexo = B.Sexo);



## Consulta Aninhada

*

 CC BY-NC-ND 4.0 Bloco SELECT completo na cláusula WHERE de outra consulta, denominada consulta externa I EXISTS ( NOT EXISTS ) ! verifica se o resultado da consulta interna é conjunto vazio SELECT A.CPF, A.Nome FROM PROFESSOR A WHERE NOT EXISTS (SELECT FROM DEPARTAMENTO B WHERE A.Departamento = B.Numero AND B.Nome = 'Pesquisa');

Retorna CPF e nome dos professores que não trabalham no departamento de nome Pesquisa



## Agregação

 CC BY-NC-ND 4.0 rupadas GROUP BY ! agrupa múltiplas linhas em uma utilizando função de agregação I COUNT ! conta o número de linhas agrupadas I SUM ! soma o valor na coluna de linhas agrupadas I MAX ! retorna o valor máximo na coluna de linhas ag I MIN ! retorna o valor mínimo na coluna de linhas agrupadas I AVG ! retorna a média dos valores na coluna de linhas agrupadas Funções de agregação não têm efeito em linhas com colunas participantes da função com valor NULL



## Agregação

 CC BY-NC-ND 4.0 COUNT( * ), SUM(Salario) Sexo = 'F'; Departamento, COUNT( * ), SUM(Salario), MAX(Salario), MIN(Salario), AVG(Salario) PROFESSOR Departamento;

Exemplos:

SELECT

FROM PROFESSOR

WHERE

Retorna o número de professores do sexo feminino e o salário pago a elas

SELECT

FROM

GROUP BY

Para cada departamento retorna seu número, a quantidade de professores, a soma de salários, o salário máximo e mínimo e a média salarial



## Agregação

 CC BY-NC-ND 4.0 HAVING ! remove linhas do resultado agregado de acordo com condição imposta sobre as funções de agregação SELECT Departamento, COUNT( * ), SUM(Salario) FROM PROFESSOR GROUP BY Departamento HAVING AVG(Salario) &gt; 8000.00; Para cada departamento retorna seu número, a quantidade de professores e a soma de salários, desde que a média salarial do departamento seja maior que 8000,00



## Resumo de Instruções

INSERT INTO &lt;tabela&gt; [(&lt;lista de atributos&gt;)] VALUES (&lt;lista de valores&gt;);

UPDATE &lt;tabela&gt; SET &lt;lista de atribuicoes&gt; [WHERE &lt;condicao&gt;];

DELETE FROM &lt;tabela&gt; [WHERE &lt;condicao&gt;];

SELECT

FROM

[WHERE &lt;condicao&gt;]



[GROUP BY &lt;atributos de agrupamento&gt;]

[HAVING &lt;condicao de grupo&gt;]



CC BY-NC-ND 4.0

[ORDER BY &lt;lista de atributos&gt;];



## Referências Bibliográficas

- [1] Elmasri, Ramez; Navathe, Sham. Fundamentals of Database Systems . 7ed. Pearson, 2016.
- [2] Silberschatz, Abraham; Korth, Henry F.; Sudarshan, S. Database System Concepts . 6ed. McGraw-Hill, 2011.
- [3] Date, Christopher J. An Introduction to Database Systems . 8ed. Pearson, 2004.



## Sistemas de Banco de Dados

Fundamentos em Bancos de Dados Relacionais



Material distribuído sob licença CC BY-NC-ND 4.0

Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International

## modelo er estendido



## Modelo ER Estendido (EER)

 Modelo entidade-relacionamento (ER) aprimorado, incorporando conceitos adicionais de modelagem semântica de dados I Acrônimo do inglês para E nhanced E ntityR elationship I Apresenta requisitos mais complexos e precisos I Herança I Supertipo e subtipo I Restrições complexas I Generalização e especialização

CC BY-NC-ND 4.0





## EER: Supertipos e Subtipos

 CC BY-NC-ND 4.0 relacionamentode Entidades podem possuir subtipos que precisam de representação explícita Subtipo ou subclasse são subagrupamentos de uma entidade denominada supertipo ou superclasse I Orelacionamento entre essas entidades é denominado supertipo/subtipo , superclasse/subclasse ou classe/subclasse Professor I Doutor I Mestre I Bacharel I Mensalista Professor (supertipo) I Doutor (subtipo) I Mestre (subtipo) I Bacharel (subtipo) I Mensalista (subtipo)

- I Horista
- I Horista (subtipo)



## EER: Supertipos e Subtipos





## EER: Herança de Tipo

Ocorre em situações em que a entidade de uma subclasse herda todos os atributos e relacionamentos da classe

- I Uma entidade na subclasse possui atributos específicos, assim como valores de atributos da classe
- CC BY-NC-ND 4.0 I Exemplo ! subclasse Doutor possui atributo próprio Tese e vários outros atributos herdados da superclasse Professor , como CPF





## EER: Especialização

Definição de um conjunto de subclasses de uma entidade com base em alguma característica específica

 CC BY-NC-ND 4.0 Caso 1 ! Titulação Professor I Doutor I Mestre I Bacharel Caso 2 ! Forma de remuneração Professor I Mensalista I Horista



## EER: Especialização





## EER: Especialização

Definição por Condição ! entidades que serão subclasse são definidas a partir de uma condição aplicada a um atributo







## EER: Generalização

Definição de um tipo de entidade geral com base em entidades específicas

- I Identifica-se características comuns e generaliza-se em uma classe





Carro e Caminhão possuem vários atributos comuns





## EER: Generalização

Carro e Caminhão podem ser generalizadas, passando a ser subclasses da classe generalizada Veículo







## EER: Restrição

Característica limitadora da participação de entidades em subclasses

Disjunção ! uma entidade pode ser membro de no máximo uma das subclasses

- I Uma especialização definida por um atributo de valor único implica em uma restrição de disjunção







## EER: Restrição

Sobreposição ! uma entidade pode ser membro de mais de uma subclasse







## EER: Restrição

Participação ! determina a participação de uma entidade em subclasses

- I Especialização Parcial ! entidade não precisa ser membro de subclasses
- I Especialização Total ! toda entidade precisa ser membro de pelo menos uma subclasse na especialização







## EER: Reticulado e Herança

 CC BY-NC-ND 4.0 Uma subclasse pode ser superclasse de outras subclasses, formando um reticulado de especializações I Hierarquia Estrita ! cada subclasse tem apenas uma superclasse, resultando em uma estrutura de árvore I Reticulado ! cada subclasse pode pertencer a diferentes superclasses, resultando em uma estrutura emaranhada complexa Subclasses podem herdar atributos e relacionamentos de múltiplas classes I Herança Simples ! herança de uma única classe I Herança Múltipla ! herança de múltiplas classes 



## EER: Especialização x Generalização



 idassubclasses CC BY-NC-ND 4.0 egaramesma Especialização ! processo de refinamento conceitual de cima para baixo ( top-down ) em que se inicia com uma entidade e depois são defin pela especialização sucessiva Generalização ! processo de refinamento conceitual de baixo para cima ( bottom-up ) em que pela síntese conceitual é possível se ch hierarquia ou reticulado da alcançada pela outra direção Estruturalmente o resultado de ambos os processos são idênticos





## EER: União

Subclasse representa uma coleção de entidades, um subconjunto da união de entidades distintas

Exemplo ! Proprietário pode ser um Banco , uma Empresa ou uma Pessoa

## Proprietário (união)

- I Banco (entidade)
- I Pessoa (entidade)
- I Empresa (entidade)

Proprietário herda atributos e relacionamentos de Banco Empresa , e Pessoa

CC BY-NC-ND 4.0





## EER: União





## EER: Projeto Conceitual

 CC BY-NC-ND 4.0 raglomeraçãodo Em um projeto conceitual há um processo de refinamento iterativo até que o projeto mais adequado seja alcançado Existem diretrizes para direcionar escolhas em projetos: 1. Representar apenas subclasses necessárias para evita modelo conceitual 2. Subclasse com poucos atributos são candidatas à mesclagem com a superclasse I Atributos específicos da subclasse teriam valores NULL para entidades não membros da subclasse I Atributo de tipo pode especificar se uma entidade é um membro da subclasse 



## EER: Projeto Conceitual

 tejustifique CC BY-NC-ND 4.0 ecitadanenhuma 3 União deve ser evitada, a menos que a situação definitivamen esse tipo de construção 4 A escolha de restrições de disjunção, sobreposição e totalidade sobre a especialização deve ser regida pelas regras do minimundo I Se na especificação do minimundo não é explicitament restrição, o padrão menos restritivo de sobreposição parcial deve ser adotado



## Referências Bibliográficas

- [1] Elmasri, Ramez; Navathe, Sham. Fundamentals of Database Systems . 7ed. Pearson, 2016.
- [2] Silberschatz, Abraham; Korth, Henry F.; Sudarshan, S. Database System Concepts . 6ed. McGraw-Hill, 2011.
- [3] Date, Christopher J. An Introduction to Database Systems . 8ed. Pearson, 2004.



## Sistemas de Banco de Dados

Fundamentos em Bancos de Dados Relacionais



Material distribuído sob licença CC BY-NC-ND 4.0

Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International

## projeto físico

## Projeto Físico de BD

## Fator de Impacto

- I Característica da consulta
- I Frequência de execução
- I Tempo de execução
- I Exclusividade em campo

 CC BY-NC-ND 4.0 dos Criação de estrutura apropriada para armazenamento de dados com foco em desempenho na execução de consultas e transações Decisão I Recuperação de da I Que arquivos são acessados? I Que campos estão especificados? I Junção e seleção ! indexação I Condição em junção e seleção ? I = ! multiplicidade de índices I , ! limita uso de índice I &lt; GLYPH&lt;20&gt; GLYPH&lt;21&gt; &gt; ! limitação índice hash



## Projeto Físico de BD

 CC BY-NC-ND 4.0 os Criação de estrutura apropriada para armazenamento de dados com foco em desempenho na execução de consultas e transações Fator de Impacto I Característica da consulta I Frequência de execução I Tempo de execução I Exclusividade em campo Decisão I Atualização de dad I Que arquivos são atualizados? I Que operações são realizadas? I Que campos estão especificados? I Seleção ! considerar indexação I Modificação ! evitar indexação I Condição em seleção ? I = ! multiplicidade de índices

- I , ! limita uso de índice
- I &lt; GLYPH&lt;20&gt; GLYPH&lt;21&gt; &gt; ! limitação índice hash



## Projeto Físico de BD

 CC BY-NC-ND 4.0 adedetempo? Criação de estrutura apropriada para armazenamento de dados com foco em desempenho na execução de consultas e transações Fator de Impacto I Característica da consulta I Frequência de execução I Tempo de execução I Exclusividade em campo Decisão I Execuções por unid I Frequente ! considerar indexação para recuperação frequente e evitar indexação para atualização frequente I Pareto ! 80% do processamento é consumido por 20% das consultas e transações I Top 20% ! considerar indexação para as de recuperação e evitar indexação para as de atualização



## Projeto Físico de BD

 CC BY-NC-ND 4.0 ximoesperadopara Criação de estrutura apropriada para armazenamento de dados com foco em desempenho na execução de consultas e transações Fator de Impacto I Característica da consulta I Frequência de execução I Tempo de execução I Exclusividade em campo Decisão I Tempo médio e má execução? I Que consultas e transações tem forte restrição de tempo de execução? I Críticas ! considerar indexação para recuperação e evitar indexação para atualização



## Projeto Físico de BD

Criação de estrutura apropriada para armazenamento de dados com foco em desempenho na execução de consultas e transações

## Fator de Impacto

- I Característica da consulta
- I Frequência de execução
- I Tempo de execução
- I Exclusividade em campo

 CC BY-NC-ND 4.0 xclusivos? Decisão I Que campos são e

- I Campos exclusivos são usados frequentemente em junção e seleção
- I Considerar indexação para campos exclusivos



## Projeto Físico de BD

 CC BY-NC-ND 4.0 Muitas decisões de projeto físico envolvem indexação CREATE [UNIQUE] INDEX &lt;nome&gt; ON &lt;tabela&gt; ( &lt;coluna&gt; [&lt;ORDEM&gt;] {, &lt;coluna&gt; [&lt;ORDEM&gt;]} ) [CLUSTER]; I unique ! campo de indexação será exclusivo I cluster ! índice será um arquivo ordenado pelo campo de indexação I ordem ! forma de ordenação do campo de indexação I asc ! ordenação ascendente I desc ! ordenação descendente



## Projeto Físico de BD

-  CC BY-NC-ND 4.0 Desnormalização ! modificação no projeto lógico para se obter mais eficiência no processamento de consultas e transações I Duplicação de atributos ! inclusão de atributos de uma tabela em outra I Evita operações de junção entre as tabelas I Introduz redundância em tabelas I Exemplo: introduzir o atributo Nome da tabela departamento na tabela professor evita a necessidade de junção entre as tabelas se a consulta por Nome de departamento e Nome de professor for frequentemente realizada PROFESSOR CPF Nome Sexo Salario Depto NomeDepto DEPARTAMENTO Numero Nome Superior



## Ajuste de BD

CC BY-NC-ND 4.0 sultasetransações

 Todo projeto precisa de ajustes ao ser executado Sintonia (Tuning) ! processo de ajuste contínuo do projeto físico I Monitora e revisa decisões de projeto I Objetivo ! redução do tempo de processamento de con I Métricas ! conjunto de medidas usadas no monitoramento I Processamento ! tempo de otimização e execução de consultas e transações I Armazenamento ! espaços ocupados por pools de bu ff er , tabelas ( tablespaces ) e índices ( indexspaces ) I I/O ! # paginações em disco por unidade de tempo I Concorrência ! taxa de vazão ( throughput ) de transações, de emissão de comandos de bloqueio, e de registro em log I Índice ! # níveis, # nós folha não contíguos



## Ajuste de BD

 DBAs monitoram métricas para realizar ajustes e evitar problemas: I Desperdício ! tamanho de bu ff ers inadequados I Sobrecarga ! logging e dumping desnecessários I Aumento de Concorrência ! disputa excessiva por bloq I Ineficiência ! alocação inadequada de discos, bu ff ers e processos Tais ajustes podem ocorrer de diferentes formas I Sintonia de Índice ! criação, remoção e reorganização de índices I Sintonia de Projeto ! alterações no projeto lógico

- I Sintonia de Consulta ! reescrita de consultas

CC BY-NC-ND 4.0 ueios 



## Sintonia de Índice

CC BY-NC-ND 4.0 alizados

 Avaliação dos requisitos de projeto físico para reorganizar arquivos e índices I Criação ! consultas e transações podem estar demorando a serem executadas por ausência de índice I Remoção ! índices podem estar sendo pouco utilizados I Reorganização ! índices podem estar sendo muito atu I Exclusão ! blocos de índice com espaço desperdiçado I Inclusão ! overflow excessivo em índice agrupado I Opções de indexação variam em soluções de SGBD comerciais I Sybase ! índices de agrupamento esparsos em B+ Trees I Ingress ! índices de agrupamento ISAM esparsos ou B+ Trees densos I Oracle ! índices de agrupamento densos



## Sintonia de Projeto

 CC BY-NC-ND 4.0 o Avaliação dos requisitos de projeto físico para modificação dos projetos conceitual e lógico I Duplicação de Atributos ! inclusão de atributos de uma tabela em outra PROFESSOR CPF Nome Sexo Salario Depto NomeDepto DEPARTAMENTO Numer Nome Superior I Particionamento Vertical ! divisão de atributos de uma tabela em múltiplas tabelas com mesma chave primária em relacionamento 1 : 1 PROFESSOR CPF Nome Salario PROFESSOR2 CPF Sexo Depto



## Sintonia de Projeto

Avaliação dos requisitos de projeto físico para modificação dos projetos conceitual e lógico

- I Particionamento Horizontal ! distribuição de tuplas de uma tabela em múltiplas tabelas com os mesmos atributos

|         CPF | Nome            | Sexo   |   Salario |   Departamento |
|-------------|-----------------|--------|-----------|----------------|
| 12345678900 | Roberto Machado | M      |      1200 |              1 |
| 12345678901 | Manuela Costa   | F      |      2700 |              3 |

|         CPF | Nome                 | Sexo   |   Salario |   Departamento |
|-------------|----------------------|--------|-----------|----------------|
| 21345678900 | CC Carlos A. Martins | M      |      3200 |              1 |
| 32145678900 | Ana Maria Freitas    | F      |      7500 |              2 |

CC BY-NC-ND 4.0

 PROFESSOR PROFESSOR TOP



## Sintonia de Consulta

 CC BY-NC-ND 4.0 consulta Avaliação dos requisitos de projeto físico para reescrever consultas I Indícios ! sinais de que consultas precisam ser reescritas I Plano de Execução ! índices relevantes não estão sendo usados I Paginação ! emissão de muitas solicitações de I/O I Casos Típicos ! situações que demandam reescrita de I Parsing ! ordem aleatória de tabelas no FROM e operações no WHERE I Comparação ! NULL, substring e campos de domínios diferentes SELECT A.CPF, B.Nome FROM PROFESSOR A, DEPARTAMENTO B WHERE A.Depto IS NOT NULL AND B.Nome LIKE '%TI%' AND A.Salario = B.Numero;



## Sintonia de Consulta

 lta CC BY-NC-ND 4.0 Avaliação dos requisitos de projeto físico para reescrever consultas I Casos Típicos ! situações que demandam reescrita de consu I Consultas Aninhadas ! operadores all , any some in , , e exists SELECT CPF, Nome FROM PROFESSOR WHERE Depto IN (SELECT Numero FROM DEPARTAMENTO); SELECT A.CPF, A.Nome FROM PROFESSOR A WHERE EXISTS (SELECT * FROM DEPARTAMENTO B WHERE A.Depto = B.Numero); I Deduplicação ! operador distinct SELECT DISTINCT Nome FROM PROFESSOR;



## Sintonia de Consulta

 lta CC BY-NC-ND 4.0 Avaliação dos requisitos de projeto físico para reescrever consultas I Casos Típicos ! situações que demandam reescrita de consu I Condição Disjuntiva ! operador or SELECT CPF, Nome FROM PROFESSOR WHERE Sexo = 'M' OR Salario &gt; 2000,00; SELECT CPF, Nome FROM PROFESSOR WHERE Sexo = 'M' UNION SELECT CPF, Nome FROM PROFESSOR WHERE Salario &gt; 2000,00;



## Sintonia de Consulta

 lta CC BY-NC-ND 4.0 Avaliação dos requisitos de projeto físico para reescrever consultas I Casos Típicos ! situações que demandam reescrita de consu I Condição Complexa ! operadores and e or SELECT CPF, Nome FROM PROFESSOR WHERE Depto = 1 AND ((Salario BETWEEN 1000,00 AND 2000,00) OR (Salario BETWEEN 5000,00 AND 7000,00)); SELECT CPF, Nome FROM PROFESSOR WHERE Depto = 1 AND (Salario BETWEEN 1000,00 AND 2000,00) UNION SELECT CPF, Nome FROM PROFESSOR WHERE Depto = 1 AND (Salario BETWEEN 5000,00 AND 7000,00);



## Sintonia de Consulta

 lta CC BY-NC-ND 4.0 Avaliação dos requisitos de projeto físico para reescrever consultas I Casos Típicos ! situações que demandam reescrita de consu I Consulta Complexa ! subconsultas SELECT A.CPF, A.Nome FROM PROFESSOR A WHERE A.Salario &gt; (SELECT AVG(B.Salario) FROM PROFESSOR B WHERE A.Depto = B.Depto); SELECT Depto, AVG(Salario) AS Media INTO TEMP FROM PROFESSOR GROUP BY Depto; SELECT A.CPF, A.Nome FROM PROFESSOR A, TEMP B WHERE A.Salario &gt; B.Media AND A.Depto = B.Depto;



## Referências Bibliográficas

- [1] Elmasri, Ramez; Navathe, Sham. Fundamentals of Database Systems . 7ed. Pearson, 2016.
- [2] Silberschatz, Abraham; Korth, Henry F.; Sudarshan, S. Database System Concepts . 6ed. McGraw-Hill, 2011.
- [3] Date, Christopher J. An Introduction to Database Systems . 8ed. Pearson, 2004.



## Sistemas de Banco de Dados

Fundamentos em Bancos de Dados Relacionais



Material distribuído sob licença CC BY-NC-ND 4.0

Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International

## organização de dados



## Organização de Dados



1

GLYPH&lt;1&gt;

GLYPH&lt;1&gt;

GLYPH&lt;1&gt;

 dos CC BY-NC-ND 4.0 minimundo,tais A forma como dados são dispostos em memória secundária impacta o desempenho do SGBD para recuperação e manipulação desses da I Tipicamente dados são organizados como arquivos de registros Registro ! coleção de valores relacionados a fatos sobre o como atributos, instâncias de entidades e relacionamentos 12345678900 Roberto Machado M 1200.00 1 Arquivo ! coleção de registros relacionados 12345678900 Roberto Machado M 1200.00 32145678900 Ana Maria Freitas F 7500.00 2



Registros devem ser organizados de forma a serem rapidamente localizados



## Organização de Dados

GLYPH&lt;1&gt;

GLYPH&lt;1&gt;

GLYPH&lt;1&gt;

 CC BY-NC-ND 4.0 ivo Um arquivo possui um cabeçalho (descritor) contendo metadados úteis aos programas que acessam seus registros I Ordem, tipo e tamanho de campos dos registros I Endereços dos blocos que armazenam registros do arqu I Códigos de caracteres especiais, como separadores de campos R 1 R 2 R 3 RN Cabeçalho



## Arquivos de Registros

Cada valor de um registro está restrito a um tipo de dado , sendo que o número de bytes para cada tipo é fixo, dependendo do sistema computaci

CC BY-NC-ND 4.0

 I Booleano : 1 byte I Inteiro : 4 bytes I Número real : 4 bytes I Inteiro longo : 8 bytes I Data : 10 bytes (formato DD-MM-AAAA) I String : n bytes, onde n é o número de caracteres

- I BLOB : p + n bytes, onde p é o tamanho do ponteiro no registro para o endereço de bloco onde o objeto binário de tamanho n está armazenado

 onal



## Arquivos de Registros

 CC BY-NC-ND 4.0 Arquivos podem ser compostos por registros de tamanho : I Fixo ! cada registro no arquivo tem o mesmo tamanho I Variável ! registros no arquivo possuem tamanhos diferentes I Campos de tamanho variável ! VARCHAR, TEXT I Campos opcionais ! NULL I Campos multivalorados I Arquivos mistos com registros de instâncias de entidades diferentes Tipicamente, todos os registros em um arquivo referem-se às instâncias de uma mesma entidade

- I Arquivo Professor ! Entidade Professor



## Arquivos de Registros

 CC BY-NC-ND 4.0 Um arquivo é alocado em diferentes blocos de disco, sendo que seus registros podem estar alocados em um ou vários blocos I Não Espalhado ! registro não pode atravessar o limite de um bloco Bloco i R1 R2 Bloco i+1 R3 R4 I Espalhado ! registro é armazenado em múltiplos blocos I Ponteiro no fim de cada bloco aponta para o bloco de continuidade do registro Bloco i R1 R2 R3 GLYPH&lt;15&gt; Bloco i+1 R3 R4 R5



## Arquivos de Registros

 disco CC BY-NC-ND 4.0 Blocagem , ou Fator de Bloco , ou Fator de Blocagem de um arquivo é a quantidade de registros desse arquivo que cabem em um bloco de Considere: I Blocos com t bytes I Registros de r bytes, sendo r GLYPH&lt;20&gt; t I Fator de Bloco ! F = j t r k Em arquivo com registros de tamanho fixo, r é o tamanho do registro, enquanto em arquivo com registros de tamanho variável, considera-se r o tamanho médio de registros



## Arquivos de Registros

 arareduzir CC BY-NC-ND 4.0 Se r é suficientemente grande, tal que r &gt; t = 2, o espaço não usado em disco pode ser grande e o espalhamento de registros passa a ser vantajoso p esse "espaço perdido" I Espaço não usado ! U = t GLYPH&lt;0&gt; ( F GLYPH&lt;2&gt; r ) O número de blocos ( B ) necessários para armazenar um arquivo é: I B = l n F m , onde n é o número de registros do arquivo



## Arquivos de Registros

 Por exemplo, considere um arquivo de Professor armazenado em um disco com blocos de t = 4 KB , onde: I r = 185 B I n = 10 000 : Nesse caso, teremos: I F = j 4 KB 185 B k = j 4 GLYPH&lt;2&gt; 1 024 : B 185 B k GLYPH&lt;25&gt; b 22 14 ; c = 22 I U = 4 KB GLYPH&lt;0&gt; ( 22 GLYPH&lt;2&gt; 185 B ) = 4 096 : B GLYPH&lt;0&gt; 4 070 : B = 26 B

- I B = l 10 000 : 22 m GLYPH&lt;25&gt; d 454 54 ; e = 455



CC BY-NC-ND 4.0

- I Consumo de espaço ! 455 GLYPH&lt;2&gt; 4 KB = 1 820 : KB GLYPH&lt;25&gt; 1 77 ; MB



## Métodos de Acesso

 CC BY-NC-ND 4.0 clusãoderegistros, Grupo de operações que podem ser aplicadas a um arquivo I Recuperação ! localização de registros em arquivo para que valores de campos possam ser lidos e processados, sem que haja alteração nos dados I Atualização ! alteração de arquivo pela inserção ou ex ou pela modificação de valores de campos de registros A frequência da mudança em arquivos determina a frequência de execução de operações de atualização I Arquivos Estáticos ! operações de atualização são raramente executadas 

- I Arquivos Dinâmicos ! mudam com frequência de forma que operações de atualização são constantemente executadas



## Métodos de Acesso

CC BY-NC-ND 4.0 plexidade

 Muitas operações aplicadas a arquivos envolvem pesquisa I Especifica critérios que registros devem satisfazer I Tipicamente, critérios envolvem expressões booleanas I Expressões podem apresentar diferentes graus de com I Simples ! expressões booleanas simples I Exemplo: (Sexo = 'M') I Complexas ! expressões booleanas complexas I Exemplo: ((Sexo = 'M') ^ ((Salario &gt; 3.000) \_ : ( TemDependente)))



## Métodos de Acesso

CC BY-NC-ND 4.0

 SGBDs acessam registros utilizando operações representativas , em que tipicamente um registro é processado por vez I Open ! prepara arquivo para leitura ou escrita I Aloca bu ff ers para blocos I Recupera o cabeçalho do arquivo I Posiciona o ponteiro de arquivo no início do arquivo I Reset ! posiciona o ponteiro do arquivo aberto para o início do arquivo I Close ! libera bu ff ers alocados e realiza operações de limpeza de memória



## Métodos de Acesso

CC BY-NC-ND 4.0 oregistroatual

 Operações representativas I Find (Locate) ! procura o primeiro registro que satisfaça uma condição I Transfere o bloco que contém o registro para um bu ff er alocado I Posiciona o ponteiro de arquivo no registro, tornando-o I FindNext ! procura o próximo registro que satisfaça uma condição I Transfere o bloco que contém o registro para um bu ff er alocado I Posiciona o ponteiro de arquivo no registro, tornando-o o registro atual I Read (Get) ! copia o registro do bu ff er para uma variável de programa I Posiciona o ponteiro no próximo registro, tornando-o o registro atual



## Métodos de Acesso

CC BY-NC-ND 4.0 l

 Operações representativas I Delete ! remove o registro atual I Transfere o bu ff er de volta ao bloco no disco I Modify ! modifica valores de campos do registro atua I Transfere o bu ff er de volta ao bloco no disco I Insert ! insere um novo registro no arquivo I Localiza o bloco onde o registro deve ser inserido I Transfere o bloco para um bu ff er I Escreve o registro no bu ff er

- I Transfere o bu ff er de volta ao bloco no disco



## Métodos de Acesso

CC BY-NC-ND 4.0 arquivo,reposiciona-ono

 Operações representativas I Scan ! combinação das operações Find , FindNext e Read I Se uma condição é especificada I Se o ponteiro de arquivo estiver posicionado no início do primeiro registro que satisfaça a condição I Se o ponteiro de arquivo estiver posicionado em algum registro, reposiciona-o no próximo registro que satisfaça a condição I Caso contrário I Se o ponteiro de arquivo estiver posicionado no início do arquivo, reposiciona-o no primeiro registro

- I Se o ponteiro de arquivo estiver posicionado em algum registro, reposiciona-o no próximo registro



## Métodos de Acesso

 CC BY-NC-ND 4.0 njuntoderegistros Existem operações representativas de nível mais alto que podem ser aplicadas a conjuntos de registros I FindAll ! procura o conjunto de registros que satisfaça uma condição I FindOrdered ! procura, em uma ordem específica, o co que satisfaça uma condição I FindN ! procura os N primeiros registros que satisfaçam uma condição I Reorganize ! reorganiza os blocos e registros de um arquivo



## Tipos de Arquivo

 contram-se CC BY-NC-ND 4.0 em,comnovos Métodos de acesso operam de maneira diferente dependendo da forma como arquivos são organizados, especialmente de como os registros en dispostos dentro dos arquivos I Arquivo Heap (Pilha) ! registros posicionados sem ord registros acrescentados ao final do arquivo I Arquivo Sequencial ! registros posicionados ordenadamente por um ou mais campos, denominados campos de ordenação I Arquivo Hash ! registros posicionados a partir da aplicação de uma função hash sobre um ou mais campos, denominados campos hash



## Tipos de Arquivo: Heap



 CC BY-NC-ND 4.0 Arquivo organizado de forma que os registros são dispostos desordenadamente Arquivo Novo I Pesquisa ! linear, varrendo todos os registros do arquivo no pior caso I Endereço do primeiro bloco do arquivo é recuperado do cabeçalho I Começando do primeiro, cada bloco é copiado para um bu ff er , onde deve-se verificar se cada registro do bloco satisfaz os critérios de pesquisa

- I Complexidade ! O n ( ) , onde n é o número de blocos do arquivo



## Tipos de Arquivo: Heap

 CC BY-NC-ND 4.0 beçalho Inserção eficiente, mas operações de alteração demandam pesquisa para encontrar o registro a ser alterado I Inserção ! registro arquivado na ordem em que é inserido I Endereço do último bloco do arquivo é recuperado do ca I Bloco copiado para um bu ff er , onde o novo registro é acrescentado, e o bu ff er é copiado de volta ao bloco I Alteração ! pode resultar em exclusão seguida de inclusão, caso o registro aumente de tamanho I Endereço do bloco do arquivo é recuperado via pesquisa

- I Bloco copiado para um bu ff er , onde o registro é modificado, e o bu ff er é copiado de volta ao bloco



## Tipos de Arquivo: Heap



- I Marcação ! cada registro possui um byte extra, denominado marcador de exclusão. Assim, o bloco é copiado para um bu ff er , onde o marcador de exclusão do registro é modificado, e o bu ff er é copiado de volta ao bloco

 CC BY-NC-ND 4.0 Operações de exclusão resultam em desperdício de espaço no bloco, demandando reorganização periódica do arquivo GLYPH&lt;15&gt; GLYPH&lt;15&gt; GLYPH&lt;1&gt; GLYPH&lt;1&gt; GLYPH&lt;1&gt; Arquivo 5 A GLYPH&lt;1&gt; GLYPH&lt;1&gt; GLYPH&lt;1&gt; 1 C 2 B GLYPH&lt;1&gt; GLYPH&lt;1&gt; GLYPH&lt;1&gt; 8 D 4 A Removido I Exclusão ! efetuada diretamente ou por marcação I Endereço do bloco do arquivo é recuperado via pesquisa I Direta ! bloco copiado para um bu ff er , onde o registro é removido, e o bu ff er é copiado de volta ao bloco



## Tipos de Arquivo: Heap

 Arquivo Direto (Relativo) ! arquivo heap com registros de tamanho fixo, não espalhados, com blocos em alocação contígua I Acesso simples a qualquer registro pela posição relativa no arquivo I Não ajuda na pesquisa baseada em critérios I Facilita a construção de índices no arquivo

CC BY-NC-ND 4.0





## Tipos de Arquivo: Sequencial



 CC BY-NC-ND 4.0 Arquivo organizado de forma que os registros são dispostos ordenadamente Arquivo I Blocos em cilindros contíguos, minimizando tempo de busca I Pesquisa ! binária, varrendo pequena quantidade de registros se a pesquisa for feita com operadores &lt; GLYPH&lt;20&gt; = &gt; GLYPH&lt;21&gt; sobre os campos de ordenação I Blocos intermediários são recuperados e segmentos são descartados até se encontrar registros que satisfaçam os critérios de pesquisa

- I Complexidade ! O ( log 2 n ) , onde n é o número de blocos do arquivo



## Tipos de Arquivo: Sequencial

 CC BY-NC-ND 4.0 uperadoviapesquisa Operações de alteração são onerosas, pois podem demandar reorganização dos registros para preservação de ordem I Inserção ! registro deve ser inserido na posição correta I Endereço do bloco onde registro deve ser inserido é rec I Deslocam-se registros para posições subsequentes, abrindo-se espaço para o registro a ser inserido I Blocos modificados nos deslocamentos são gravados de volta no disco Bloco 1 GLYPH&lt;15&gt; Bloco 2 GLYPH&lt;15&gt; Bloco n GLYPH&lt;1&gt; GLYPH&lt;1&gt; GLYPH&lt;1&gt; GLYPH&lt;15&gt; 1 C GLYPH&lt;1&gt; GLYPH&lt;1&gt; GLYPH&lt;1&gt; 2 B 3 F GLYPH&lt;1&gt; GLYPH&lt;1&gt; GLYPH&lt;1&gt; 4 A 5 A GLYPH&lt;1&gt; GLYPH&lt;1&gt; GLYPH&lt;1&gt; 6 E





## Tipos de Arquivo: Sequencial

## Existem alternativas para desonerar a inclusão



 CC BY-NC-ND 4.0 on I Espaços Vazios ! diminui deslocamentos, mas problema reaparece com espaços vazios totalmente preenchidos Bloco 1 GLYPH&lt;15&gt; Bloco 2 GLYPH&lt;15&gt; Bloc GLYPH&lt;1&gt; GLYPH&lt;1&gt; GLYPH&lt;1&gt; Arquivo 1 C GLYPH&lt;1&gt; GLYPH&lt;1&gt; GLYPH&lt;1&gt; 3 F GLYPH&lt;1&gt; GLYPH&lt;1&gt; GLYPH&lt;1&gt; 4 A 5 A GLYPH&lt;1&gt; GLYPH&lt;1&gt; GLYPH&lt;1&gt; I Arquivo Temporário (Overflow) ! arquivo heap onde novos registros são inseridos a um baixo custo I Periodicamente arquivo temporário é mesclado ao arquivo principal

- I Maior complexidade de pesquisa com necessidade de pesquisa linear no arquivo temporário caso o registro não seja encontrado no arquivo principal



## Tipos de Arquivo: Sequencial

CC BY-NC-ND 4.0 nação

 Alteração no registro pode demandar seu reposicionamento I Alteração ! dependente da condição de pesquisa e do campo a ser alterado I Endereço do bloco do arquivo é recuperado via pesquisa I Pesquisa binária ! critério envolver os campos de orde I Pesquisa linear ! caso contrário I Bloco copiado para um bu ff er I Campo de ordenação não modificado ! modifica-se o registro no bu ff er , copiando o bu ff er de volta ao bloco I Campo de ordenação modificado ! deslocam-se registros gravando todos os blocos modificados

- I Exclusão ! igualmente dependente da condição de pesquisa



## Tipos de Arquivo: Hash

Arquivo organizado de forma que os registros são distribuídos em blocos de acordo com uma função hash





- CC BY-NC-ND 4.0 1 2 4 5 6 8 f ( x ) Bloco 1 2 n Bloco 1 I Pesquisa ! tempo constante, localizando diretamente o bloco do registro se a pesquisa for feita com operador = sobre o campo hash I Função aplicada sobre o campo hash calcula o endereço do bloco do registro
- I Complexidade ! O ( 1 )



## Tipos de Arquivo: Hash

CC BY-NC-ND 4.0

 Operações de alteração de registros eficientes I Inclusão ! pode gerar colisão e necessidade de expansão de arquivo I Aplica-se a função hash sobre o campo hash para calcular o endereço do bloco I Bloco copiado para um bu ff er , onde o novo registro é acrescentado, e o bu ff er é copiado de volta ao bloco I Alteração ! dependente da condição de pesquisa e do campo alterado I Endereço do bloco do arquivo é recuperado via pesquisa em tempo constante I Bloco copiado para um bu ff er I Campo hash não modificado ! modifica-se o registro no bu ff er , copiando o bu ff er de volta ao bloco I Campo hash modificado ! desloca-se o registro para outro bloco gravando os dois blocos modificados

- I Exclusão ! igualmente dependente da condição de pesquisa



## Tipos de Arquivo: Hash

 CC BY-NC-ND 4.0 auniforme, Funções hash podem ser implementadas de formas diferentes I Idealmente devem ser mantidas em memória primária, tornando muito eficiente o mapeamento de valores I Implementações robustas distribuem valores de maneir consumindo pouca memória primária I Existem dois problemas muito comuns em implementações hash I Colisão ! diferentes valores são mapeados para o mesmo endereço, que já pode estar ocupado I Expansão ! não há mais endereços disponíveis para armazenamento de registros e o espaço de endereçamento precisa ser expandido



## Tipos de Arquivo: Hash



 CC BY-NC-ND 4.0 rodechaves Hashing Universal ! mapeia conjunto de chaves de tamanho variável para espaço de tamanho m , tal que a probabilidade de colisão é 1 = m Chave 3 1 7 2 f ( x ) Bucket 1 2 3 4 5 I Colisão ! problema frequente quando n GLYPH&lt;25&gt; m ou n GLYPH&lt;21&gt; m , onde n é o núme I Endereçamento Aberto I Lista Encadeada I Hash Múltiplo I Fator de Carga ! n m = (max 0.75) I Expansão ! fundamental para evitar degradação da estrutura, proveniente do grande número de colisões

- I Múltiplas soluções, da reconstrução até o uso de múltiplas funções hash



## Tipos de Arquivo: Hash



 CC BY-NC-ND 4.0 Hashing Perfeito ! mapeia conjunto fixo de chaves para espaço de tamanho m , tal que não haja colisão f ( x ) 1 2 3 4 5 I Funções ocupam mais espaço em memória, com complexidade linear O n ( ) I Mínimo ! n = m , onde n é o número de chaves I Ordem preservada ! GLYPH&lt;210&gt; ( n log n ) I Ordem não preservada ! 1 44 : n I Expansão ! expandir significa reconstruir, já que conjunto de chaves é fixo I Hashing perfeito dinâmico pode ser a solução, mas complexa e de difícil implementação



## Referências Bibliográficas

- [1] Elmasri, Ramez; Navathe, Sham. Fundamentals of Database Systems . 7ed. Pearson, 2016.
- [2] Silberschatz, Abraham; Korth, Henry F.; Sudarshan, S. Database System Concepts . 6ed. McGraw-Hill, 2011.
- [3] Date, Christopher J. An Introduction to Database Systems . 8ed. Pearson, 2004.



## Sistemas de Banco de Dados

Fundamentos em Bancos de Dados Relacionais



Material distribuído sob licença CC BY-NC-ND 4.0

Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International

## modelo de dados



## Estrutura de BD

CC BY-NC-ND 4.0

 Composta por tipos, relacionamentos e restrições aplicados aos dados I Abstração de Dados I Estrutura do BD percebida de maneira diferente por usuários de acordo com diferentes níveis de detalhamento I Abordagem de BD deve ocultar detalhes de organização e armazenamento dos dados I Fornece recursos essenciais para a compreensão dos dados e de seus relacionamentos I Modelo de Dados ! oferece meios necessários para se alcançar a abstração



## Modelo de Dados

CC BY-NC-ND 4.0 uperaçãodedados

 Estrutura lógica que determina a forma como os dados são armazenados, organizados e manipulados I Coleção de conceitos que descrevem a estrutura do BD I Incorpora operações para especificar atualização e rec I Exemplo ! inserir, remover, modificar ou recuperar I Define o comportamento de uma determinada aplicação



## Modelo de Dados

CC BY-NC-ND 4.0

 Oferece diferentes níveis de abstração: I Conceitual ! alto nível de abstração I Representa a estrutura como os usuários a percebem I Conceitos ! entidade, atributo e relacionamento I Representativo ! nível intermediário de abstração I Também conhecido como modelo de implementação I Representa a estrutura detalhando aspectos de implementação I Oculta detalhes de armazenamento físico I Conceitos ! objeto, relação, tupla e coluna I Físico ! baixo nível de abstração I Representa a estrutura detalhando aspectos de armazenamento físico

- I Conceitos ! arquivo, registro, campo, índice



## Modelo de Dados: Conceitual

## Entidade ! ente (objeto) do universo de discurso



Atributo ! propriedade que caracteriza uma entidade



CC BY-NC-ND 4.0 ento





## Modelo de Dados: Conceitual

 Relacionamento ! associação entre duas ou mais entidades





## Modelo de Dados: Representativo

CC BY-NC-ND 4.0

- I Associação entre registros ! ligação

 Existem diferentes modelos representativos I Hierárquico I BD ! coleção de árvores formando uma floresta I Registro ! nó da árvore I Associação entre registros ! aresta da árvore I Umnófilho só pode ter um pai ( 1:N ) I Rede I Extensão do modelo hierárquico I Permite associações N:N I Objeto I BD ! coleção de objetos I Registro ! objeto

- I Próximo ao modelo de dados conceitual



## Modelo de Dados: Representativo

CPF

CC BY-NC-ND 4.0

 Existem diferentes modelos representativos I Relacional I BD ! coleção de relações (elementos tabulares) I Registro ! tupla (linha) I Associação entre registros ! relacionamentos I Embasamento em lógica de predicados e na teoria dos conjuntos I Amplamente adotado em SGBDs comerciais baseados em transações I Consolidado, com alto desempenho na execução de operações básicas PROFESSOR Nome Sexo Salario Departamento DEPARTAMENTO Numero Nome



## Modelo de Dados: Físico

| Ponteiro                   | Departamento               |
|----------------------------|----------------------------|
| #00                        | 1                          |
| #20                        | 2                          |
| #30                        | 3                          |
| GLYPH<1> GLYPH<1> GLYPH<1> | GLYPH<1> GLYPH<1> GLYPH<1> |
| #FF                        | N                          |

CC BY-NC-ND 4.0

 Descreve detalhes de armazenamento de dados em memória I Formatos e ordenação de registros em arquivos I Organização dos dados em arquivos em memória secundária I Caminhos de acesso alternativos para recuperação rápida de registros PROFESSOR ÍNDICE

| CPF                        | Nome                       | Sexo                       | Salario                    | BY-NC-ND Departamento      | #                          |
|----------------------------|----------------------------|----------------------------|----------------------------|----------------------------|----------------------------|
| 12345678900                | Wladmir Roberto Machado    | M                          | 1200.00                    | 1                          | 00                         |
| 21345678900                | Carlos A. Martins          | M                          | 3200.00                    | 1                          | 10                         |
| 32145678900                | Ana Maria Freitas          | F                          | 7500.00                    | 2                          | 20                         |
| 12345678901                | Manuela Costa              | F                          | 2700.00                    | 3                          | 30                         |
| 52345678902                | Luiz A. Barbosa            | M                          | 5300.00                    | 3                          | 40                         |
| 97345671200                | CC Rebeca Lins Rêgo        | F                          | 6800.00                    | 3                          | 50                         |
| GLYPH<1> GLYPH<1> GLYPH<1> | GLYPH<1> GLYPH<1> GLYPH<1> | GLYPH<1> GLYPH<1> GLYPH<1> | GLYPH<1> GLYPH<1> GLYPH<1> | GLYPH<1> GLYPH<1> GLYPH<1> | GLYPH<1> GLYPH<1> GLYPH<1> |
| 68345618900                | Amanda Ramirez             | F                          | 1700.00                    | N                          | FF                         |



## Referências Bibliográficas

- [1] Elmasri, Ramez; Navathe, Sham. Fundamentals of Database Systems . 7ed. Pearson, 2016.
- [2] Silberschatz, Abraham; Korth, Henry F.; Sudarshan, S. Database System Concepts . 6ed. McGraw-Hill, 2011.
- [3] Date, Christopher J. An Introduction to Database Systems . 8ed. Pearson, 2004.



## Sistemas de Banco de Dados

Fundamentos em Bancos de Dados Relacionais



Material distribuído sob licença CC BY-NC-ND 4.0

Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International

## introdução



## Sistemas de Banco de Dados (SBD)

 CC BY-NC-ND 4.0 "Sistemas de banco de dados referem-se ao conjunto de dados relacionados e sua respectiva forma de acesso e organização... São compostos por uma coleção de dados organizados , uma estrutura lógica determinando a forma como os dados são armazenados, organizados e manipulados, e um software que provê acesso aos dados a usuários e aplicações." Elmasri &amp; Navathe, 2016 I Coleção de Dados ! banco de dados I Estrutura Lógica ! modelo de dados I Software ! sistema gerenciador de banco de dados



## Sistemas de Banco de Dados (SBD)

Usuários e aplicações interagem com o sistema submetendo consultas consultas são interpretadas pelo sistema, que realiza otimizações necessárias para sua correta execução

O próprio sistema decide quais dados são necessários para responder uma consulta e se encarrega de recuperálos a partir dos repositórios sob seu controle

CC BY-NC-ND 4.0







## Banco de Dados (BD)

CC BY-NC-ND 4.0

 Coleção de dados organizados I Dados ! símbolos, sinais, códigos I Atende necessidades específicas de usuários I Presente em diferentes ambientes de negócio I Reserva de hotel I Reserva de livros em biblioteca I Visualização de catálogos de filmes I Compra de produtos em supermercado I Saque e depósito de dinheiro em caixa bancário





CC BY-NC-ND 4.0 Bilhões de produtos em catálogo Dezenas de milhões de transações diárias Atualização frequente de estoque e pedidos

## BD: Propriedades

CC BY-NC-ND 4.0

 BDs possuem características que os diferenciam de outros tipos de coleções I Finalidade ! construídos com um propósito específico I Realidade ! representam o "mundo real" I Mundo Real ! minimundo universo de discurso , I Coerência ! mantêm a coerência lógica da coleção I Compartilhamento ! provêm compartilhamento de dados



## BD: Taxonomia

CC BY-NC-ND 4.0

 BDs podem ser categorizados quanto à forma de utilização I Manual ! criado e mantido sem o uso de computadores I Exemplo ! lista telefônica (páginas amarelas) I Computadorizado ! criado e mantido com o uso de computadores I Exemplo ! The Human Genome Database (GDB)



## BD: Taxonomia

 CC BY-NC-ND 4.0 limáticos BDs também podem ser categorizados quanto à sua aplicação I Tradicional ! texto, incluindo números e registros temporais I Multimídia ! imagens, áudios e vídeos I Geográfico ! mapas, imagens de satélite e registros c I Data Warehouse ! armazém de dados utilizado no processamento analítico online (OLAP) para auxílio à tomada de decisão I Ativo (Tempo Real) ! utilizado em aplicações com rigorosos requisito de desempenho, como em processos industriais de manufatura



## BD: Abordagens

CC BY-NC-ND 4.0

 Diferentes abordagens de implementação I Processamento em Arquivo I Usuário define arquivos necessários para uma aplicação específica como parte da programação da aplicação I S istema G erenciador de B anco de D ados (SGBD) I Repositório único I Abstração de dados I Natureza autodescritiva I Compartilhamento de dados I Isolamento entre programas e dados I Suporte a múltiplas visões sobre dados

- I Processamento de transação multiusuário



## BD: Projeto

CC BY-NC-ND 4.0

 Construção de modelos para implementação I Modelo ! representação de entes e eventos reais I Etapas de implementação 1. Especificação ! descrição do minimundo 2. Análise de Requisitos ! restrições de operação 3. Projeto Conceitual ! estruturas e restrições conceituais 4. Projeto Lógico ! estruturas e restrições lógicas 5. Projeto Físico ! estruturas e restrições físicas I Revisado continuamente para que o BD reflita o estado do minimundo



## BD: Atores

 CC BY-NC-ND 4.0 asasetapasda Ator ! papel desempenhado pelos que interagem com o BD I Administrador (DBA) ! responsável pela operação e pelo cumprimento dos requisitos, atuando em todas as etapas da implementação I Projetista ! responsável pelo projeto, atuando em tod implementação I Analista ! mais presente nas etapas de projeto conceitual e lógico I Programador ! atua preponderantemente no projeto lógico I Usuário ! demandante, conhecedor do minimundo e mais presente na especificação e análise de requisitos



## Modelo de Dados

CC BY-NC-ND 4.0 uperaçãodedados

 Estrutura lógica que determina a forma como os dados são armazenados, organizados e manipulados I Coleção de conceitos que descrevem a estrutura do BD I Incorpora operações para especificar atualização e rec I Exemplo ! inserir, remover, modificar ou recuperar I Define o comportamento de uma determinada aplicação



## Sistema Gerenciador de Banco de Dados (SGBD)

CC BY-NC-ND 4.0 loSGBD

 Coleção de programas (software) que permitem aos usuários criar e manter BDs I Definir ! especificar tipos, estruturas e restrições armazenadas sob forma de metadados no catálogo (dicionário) do sistema I Construir ! armazenar dados em meio controlado pe I Manipular ! inserir, remover, modificar e recuperar dados I Compartilhar ! prover acesso simultâneo a múltiplos usuários



## SGBD: Propriedades





 CC BY-NC-ND 4.0 drões Controle de Redundância I Flexibilidade I Múltiplas interfaces I Economia de escala I Garantia de pa I Restrições de acesso I Backup e recuperação I Disponibilidade elevada I Restrições de integridade I Tempo de desenvolvimento

- I Relacionamentos complexos



## SGBD: Limitações

-  CC BY-NC-ND 4.0 ltaescalabilidade e Uso de SGBDs pode ser inadequado em algumas situações I Monousuário ! acesso por múltiplos usuários não requerido I Baixa complexidade ! aplicações muito simples e bem definidas I Requisitos rigorosos ! aplicações de tempo real, de a sistemas embarcados com capacidade de armazenamento limitada I Alta especialização ! aplicações que demandam recursos que a generalidade oferecida pelo SGBD para definição e processamento de dados não suporta I Exemplo ! funções de segurança sofisticadas
- I Custo proibitivo ! impossibilidade de investimento inicial significativo em hardware, software e treinamento



## Referências Bibliográficas

- [1] Elmasri, Ramez; Navathe, Sham. Fundamentals of Database Systems . 7ed. Pearson, 2016.
- [2] Silberschatz, Abraham; Korth, Henry F.; Sudarshan, S. Database System Concepts . 6ed. McGraw-Hill, 2011.
- [3] Date, Christopher J. An Introduction to Database Systems . 8ed. Pearson, 2004.

