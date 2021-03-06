# latex

 Esta é uma biblioteca em progresso com o intuito de facilitar a
 exportação dos dados com formatação de tabela (e imagem para os
 gráficos numa versão futura) do LaTeX.  

 As comunicações estão sendo feitas de modo que seja possível fazer
 essas comunicações simples, porém altamente configurável para os
 programadores que necessitem seguir normas específicas de formatação
 de tabelas e gráficos que não sejam necessariamente "amigáveis" com
 as da ABNT ou similares.  

 A biblioteca foi feita para trabalhar com as classes `article` e
 `abntex2` do LaTeX. Não é garantida a sua funcionalidade com as
 demais classes.  

 O resultado final é a tabela em um arquivo LaTeX que pode ser
 facilmente incluída no relatório ou trabalho com o simples
 uso de um `\input{arquivo.tex}` para a inclusão sem quebra de página
 ou um `\include{arquivo.tex}` para inclusão com quebra de página.

## Tabelas LaTeX

 Esta parte da biblioteca tem sua implementação centrada em uma
 estrutura que guarda as informações que são necessárias para a
 construção de uma tabela em LaTeX legível ao usuário conhecedor da
 linguagem, de forma que este possa facilmente modificar a tabela sem
 necessidade de horas de análise ou modificação das *strings*
 enviadas à biblioteca e reexecução do *software*, são elas:  

 - Número de colunas  

 - Número de linhas já escritas

 É usado para fazer a numeração das linhas da tabela na  forma de
 comentários, facilitando eventuais modificações desta "à mão", sem
 necessidade de modificar e reexecutar o programa para isso.

 - Ponteiro para o arquivo onde está sendo escrita a tabela  

### Funções da saída para o LaTeX

 ~~~c
 tabela_tex inicializa(const char *nome_arq, uint8_t num_colunas, const char *capt)
 ~~~

  Inicializa a estrutura, além de abrir e inicializar o arquivo,
  abrindo a tabela, centralizando, e colocando o título, caso este
  seja no cabeçalho.  

 ~~~c
 void nome_colunas(tabela_tex tabela, ...)
 ~~~

  Coloca as strings na sequência como nomes das colunas até que o
  número de colunas seja atingido e coloca uma linha horizontal em
  seguida.  

 ~~~c
 void printoneline(tabela_tex *tabela, char *format, ...)
 ~~~

 A função printa uma linha da tabela conforme especificado na string
 format, enquanto faz a separação entre as colunas pelos espaço ou
 tabulações presentes na string.  

 ~~~c
 void printoneline_v2(tabela_tex *tabela, ...)
 ~~~

 A mesma coisa que a função anterior, porém para cada coluna é
 recebida uma string format, seguida (ou não) das variáveis a serem
 impressas.

 ~~~c
 void printmultiline(tabela_tex *tabela, const uint8_t qte_linhas, char *format, ...)
 ~~~

 A função printa várias linhas da tabela conforme especificado na
 string format, enquanto faz a separação entre as colunas pelos
 espaço ou tabulações presentes na string.  

 ~~~c
 void printmultiline_v2(tabela_tex *tabela, const uint8_t qte_linhas, ...)
 ~~~

 A mesma coisa que a função anterior, porém para cada coluna é
 recebida uma string format, seguida (ou não) das variáveis a serem
 impressas.

 ~~~c
 void fechatabela(tabela_tex tabela, const char *rodape, const char *label)
 ~~~

 Fecha a tabela colocando as notas de rodapé, o label da tabela e o
 `end{table}`, além de fechar o arquivo. Caso não se queira um label
 ou notas de rodapé deve-se apenas enviar strings vazias nos
 respectivos argumentos.  

## Configurações da bilioteca

 É possível configurar a biblioteca por meio de alguns `define`
 antes de incluir a biblioteca. A configuração é feita dessa
 maneira visando a otimização de ROM por parte do executável, por não
 necessitar guardar as *strings* das configurações não utilizadas,
 além de que, por não necessitar selecionar a configuração em tempo
 de execução, há uma ligeira otimização de tempo.  

 ~~~c
#define FORCE_POSITION
 ~~~

 Adiciona um ! nas opções da tabela, "forçando" o LaTeX a colocá-la
 no lugar inserido.  

 ~~~c
#define LINHAS_ESTILIZADAS
 ~~~

 Utiliza comandos de linhas estilizadas como `\toprule` e
 `\bottomrule` ao invés do `\hline`.  

 ~~~c
#define TITULO_NO_FINAL
 ~~~

 Transfere o título para o final da tabela, no lugar das notas de
 rodapé.  

 ~~~c
#define LINHAS_VERTICAIS
 ~~~

 Coloca linhas verticais simples entre as colunas da tabela.  
