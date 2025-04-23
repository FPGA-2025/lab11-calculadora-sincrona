# Calculadora Síncrona

Agora que você já foi capaz de fazer os laboratórios anteriores, chegou a hora de fazer uma modificação na calculadora: torná-la um circuito síncrono. 

Como é explicado nas aulas, um circuito síncrono é aquele que é capaz de armazenar um estado interno por meio de registradores que são acionados por uma borda de relógio. Circuitos síncronos permitem mais possibilidades de comportamento se comparados com os combinacionais. É interessante notar que muitos dos circuitos nos próximos laboratórios serão síncronos também.

## Comportamento da calculadora

Essa calculadora terá apenas uma entrada de 8 bits, um código de operação e uma saída de 8 bits além, claro, do relógio (clk) e do reset. A principal diferença desta calculadora para a anterior é que esta possui um acumulador interno, que consegue guardar o resultado. Pode-se descrever o comportamento da calculadora de acordo com a tabela abaixo:

Operação        | Código | Entrada   | Acumulador Atual | Acumulador no próximo pulso de relógio | Saída no próx. pulso |
|---------------|--------|-----------|------------------|----------------------------------------|----------------------|
Mostrar Ent.    | 000    | 0000 1010 | 0000 0000        |     0000 0000                          | 0000 1010            |
Somar           | 001    | 0000 1010 | 0000 0000        |     0000 1010                          | 0000 0000            |
Subtrair        | 010    | 0000 0010 | 0000 1010        |     0000 1000                          | 0000 0000            |
Mostrar Ac.     | 011    | 0000 1010 | 0000 1000        |     0000 1000                          | 0000 1000            |

- Mostrar Entrada: Essa operação faz com que o valor da entrada apareça na saída no próximo pulso de relógio. O acumulador não é modificado.
- Somar: Essa operação soma o valor da entrada com o valor do acumulador. A saída, após o pulso de relógio, volta para zero.
- Subtrair: Essa operação realiza a subtração Acumulador - Entrada.  A saída, após o pulso de relógio, volta para zero.
- Mostrar Acumulador: Essa operação faz com que o valor acumulado apareça na saída no próximo pulso de relógio. O acumulador não é modificado.

Quando reset=1, o valor do acumulador deve ser zerado independentemente das outras entradas. A saída deve mostrar zero. Faça um reset assíncrono: use `@ posedge rst` na lista de sensibilidade do bloco always.

> A calculadora deve utilizar um circuito sequencial, ou seja, é necessário usar o tipo `reg` para alguns sinais. A saída, por exemplo, é um reg.

## Execução da atividade

Siga o modelo de módulo já fornecido e utilize o testbench e scripts de execução para sua verificação. Em seguida, implemente o circuito da calculadora de acordo com as especificações e, se necessário, crie outros testes para verificá-lo.

> DICA: sempre comece o teste resetando a calculadora, para evitar propagação de sinais não inicializados "xxxx".

Uma vez que estiver satisfeito com o circuito, execute o script de testes com `./run-all.sh`. Serão feitos 10 testes: cada um deles mostrará na tela `ERRO` em caso de falha ou `OK` em caso de sucesso.

## Entrega

Para entregar o projeto, basta fazer um *commit* no repositório do GitHub. O GitHub Classroom já está configurado para verificar a entrega e atribuir a nota dos testes automaticamente.

> Os testes do GitHub estão embutidos nos arquivos do laboratório. Se quiser saber mais sobre eles, veja o script de correção 'run.sh' do repositório do GitHub. Não altere os arquivos de correção!