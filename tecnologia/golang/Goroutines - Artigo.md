# How to Goroutines  
Este repositório foi criado para ajudar desenvolvedores a entender e aplicar goroutines de forma eficaz, auxiliando no desenvolvimento de aplicações concorrentes e evitando armadilhas comuns.

## Table of Contents
1. [Introduction](#introduction)  
   Antes de adentrarmos no assunto de goroutines, é importante entendermos a diferença entra [[concorrência]] e [[paralelismo]] haja vista que [[Golang]] é uma linguagem que fortemente utiliza o conceito de concorrência para criar aplicações mais performáticas.
   Concorrência e paralelismo são termos comumente usados para descrever a execução de múltiplas tarefas. Mas apesar de, as vezes, serem confudidos como a mesma coisa, eles não são pois eles representam a forma como as tarefas são gerenciadas e executadas.
   **Concorrencia**: é a capacidade de um programar lidar com múltiplas tarefas aparentemente ao mesmo tempo, mesmo que a execução dependa da troca rápida entres as tarefas permitindo que o sistema progrida em diversas tarefas sem esperar que uma termine completamente antes de iniciar a outra. 
   A **analogia** clássica para explicar esse conceito é a de imaginar um garçom em um restaurante. Ele precisa atender diversos clientes, pegar os pedidos, servir as bebidas, servir os pratos, receber o pagamento e outras coisas que as vezes ele nem é pago para fazer rsrs. Mas imagina que se ele fosse parar e esperar completar o ciclo completo de um cliente para começar a atender o próximo, a espera seria longa e o restaurante iria falir. Ao invés disso, ele alterna rapidamente entre cada cliente realizando a atividade necessária que aquele cliente depende naquele momento, assim criando a ilusão de que está atendendo todos simultaneamente, mesmo que ele dedique apenas alguns minutos a cada um por vez.
   
   **Paralelismo**: é a capacidade de executar múltiplas tarefas simultaneamente distribuindo-as entre múltiplas entidades capaz de realizar as tarefas, como os núcleos de um processador.
   O paralelismo busca um progresso simultâneo verdadeiro, utilizando os recursos de hardware disponíveis para executar diferentes partes de um programa exatamente ao mesmo tempo.
   Vamos usar outra **analogia** para entender esse conceito: Pense numa casa que precisa ser pintada urgentemente. Se o dono da casa tiver apenas um pintor, ele terá que pintar uma parede de cada vez. Mas se houver vários pintores, cada um pintando uma parede diferente ao mesmo tempo, o tempo para finalizar a tarefa será menor porque todos estão trabalhando simultaneamente para completar a tarefa.
   
   Tá, mas se a linguagem Golang foi criada recentemente e já existiam processadores multi-cores, porque os criadores optaram usar concorrência ao invés de paralelismo?
2. [O que são Goroutines?](#o-que-sao-goroutines)  
Goroutines são pequenas funções que são executadas de forma concorrente, ou seja, ao mesmo tempo que outras tarefas. (Imagine um garçom que anota o pedido, entrega ao chef e continua servindo outras mesas enquanto o pedido está sendo preparado).
Diferentemente de threads, as goroutines extremamente leves. Quando digo leve, quero dizer que elas consomem pouco recurso computacional para serem executasse e além disso o próprio go cuida de aumentar ou diminuir a quantidade de recurso computacional por elas conforme a necessidade fazendo com que seu programa seja mais eficiente. 
É necessário entender também que apesar delas serem executaras ao mesmo tempo, o go organiza todas a distribuição de todas as goroutines entre várias threads do sistema operacional. E se uma ficar paralisada por algum motivo (como aguardando uma resposta da internet), as outras continuam rodando fazendo com que o sistema continue responsivo.
3. [Criando Goroutines](#criando-goroutines)  
   3.1. Sintaxe básica (`go func()`)  
   3.2. Funções nomeadas vs. funções anônimas  
4. [Sincronização de Goroutines](#sincronizacao-de-goroutines)  
   4.1. `sync.WaitGroup`  
   4.2. `sync.Mutex` e `sync.RWMutex`  
   4.3. `sync.Once`  
5. [Comunicação com Channels](#comunicacao-com-channels)  
   5.1. Criando channels (`chan T`)  
   5.2. Envio e recebimento (`<-`)  
   5.3. Buffered vs. unbuffered channels  
   5.4. Fechando channels (`close`)  
6. [`select` e multiplexação de canais](#select-e-multiplexacao-de-canais)  
   6.1. Caso padrão (`default`)  
   6.2. Timeout com `time.After`  
   6.3. `select` em loops  
7. [Contextos e cancelamento](#contextos-e-cancelamento)  
   7.1. `context.Context`  
   7.2. Propagando cancelamento  
   7.3. Prazos (`WithTimeout`, `WithDeadline`)  
8. [Modelos de concorrência comuns](#modelos-de-concorrencia-comuns)  
   8.1. Worker pool  
   8.2. Fan-in / Fan-out  
   8.3. Pipeline  
9. [Tratamento de erros em Goroutines](#tratamento-de-erros-em-goroutines)  
   9.1. `error` e `panic`  
   9.2. Recuperação (`recover`)  
   9.3. Padrões de comunicação de erro via channels  
10. [Profiling e diagnóstico](#profiling-e-diagnostico)  
    10.1. `pprof`  
    10.2. `runtime.NumGoroutine`  
    10.3. Detectando deadlocks  
11. [Boas práticas e armadilhas comuns](#boas-praticas-e-armadilhas-comuns)  
    11.1. Evitar vazamentos de goroutine  
    11.2. Cautela com channels não lidos  
    11.3. Sincronização mínima necessária  
12. [Comparação de workloads CPU-bound vs I/O-bound](#comparacao-de-workloads-cpu-bound-vs-io-bound)  
13. [REFS](#refs)  
14. [TO-DO / Conceitos avançados](#to-do--conceitos-avancados)  
    - Pool de conexões  
    - Scheduler interno do Go  
    - Goroutines M:N