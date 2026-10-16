Minha sugestão seria utilizarmos uma **fila de prioridade baseada em Heap**, já que o objetivo é organizar os pedidos considerando a pontuação, o prazo de envio e o tamanho das embalagens.


Na aula, vimos diferentes algoritmos de ordenação, como Insertion Sort, Selection Sort, Merge Sort, Quick Sort e Heap Sort. Pelo que entendi, o Heap seria uma boa escolha para esse cenário porque permite manter o pedido mais urgente no topo da fila, sem precisar reorganizar todos os pedidos a cada nova chegada.


Também acho interessante mencionarmos o exemplo da **bilheteria apresentado na aula**, porque a lógica é parecida: não basta atender quem chegou primeiro, precisamos considerar quem tem maior prioridade.


Acredito que assim conseguimos demonstrar que entendemos os conceitos e sabemos aplicá-los ao problema proposto, sem complicar demais a solução.


Montar doc. com:


- **INTRODUÇÃO:**


- **DESENVOLVIMENTO:**

  **Problema:** explicar a dificuldade de organizar muitos pedidos com prioridades e prazos diferentes.

* **Como atualizar a fila?** Quando novos pedidos chegaram? Os prazos mudam, o sistema precisa reorganizar as prioridades?


* **Como ordenar os pedidos?** Considerando a pontuação como prioridade, o tempo restante para expedição e o tamanho

* **Como avaliar os resultados?** Comparando atrasos, quantidade de pedidos expedidos por hora e eficiência.

  **Algoritmo/Estrutura:** apresentar nossa escolha pelo Heap, explicar seu funcionamento e justificar por que seria mais adequado que uma ordenação completa.

  **Diagrama:** mostrar o caminho do pedido, desde a chegada até a expedição, passando pela definição da prioridade.

  **Trade-offs:** apresentar três vantagens e três desvantagens, relacionando com o que aprendemos sobre Big-O, desempenho, memória e estabilidade.

  **Próximos passos:** sugerir simulações para comparar os algoritmos e, futuramente, utilizar IA para melhorar a definição das prioridades.

- **CONCLUSÃO**


**Marketplace Priority Sorter (MPS)**


**Proposta de priorização inteligente de pedidos — VelozMart**


**1\. Problema**


A VelozMart precisa organizar os pedidos que aguardam expedição para reduzir atrasos e custos logísticos. Cada pedido possui uma pontuação de prioridade calculada por IA, um prazo restante e um tamanho. A solução deve definir qual pedido será processado primeiro e atualizar a fila quando novos pedidos chegarem, prazos mudarem ou ocorrerem cancelamentos.


Cenário: Com a aproximação da Black Friday, a nossa equipa de TI antecipa que o sistema atual de expedição (baseado na ordem de chegada) causará um colapso na doca de embalagem devido ao pico extremo de vendas. Precisamos urgentemente de implementar um algoritmo inteligente que priorize os pedidos em tempo real, equilibrando prazos a expirar (*dispatchWindow*), relevância comercial (*priorityScore*) e espaço físico ocupado (*sizeCategory*). O objetivo é evitar atrasos em massa, rupturas na operação logística e pesadas multas por quebra de SLA (Acordo de Nível de Serviço) durante o nosso período de maior faturação.


**2\. Algoritmo / Estrutura**


**Estrutura escolhida: Heap de prioridade com pontuação composta.**


O Heap mantém o pedido de maior prioridade no topo, permitindo identificá-lo rapidamente. A pontuação considera dois fatores:


* 70%: prioridade calculada pela IA.

* 30%: urgência do prazo.


Esses pesos são valores iniciais para teste. A categoria de tamanho será utilizada para verificar a disponibilidade de espaço na expedição.


“O motivo principal para utilizar o heap é porque o sistema não precisa de lista fechada e ordená-la apenas uma vez, tem de gerir um fluxo contínuo e imprevisível de pedidos a entrar e a sair a cada segundo.”


**Funcionamento:**


1. Receber o pedido.

2. Calcular sua prioridade e urgência.

3. Inserir o pedido no Heap.

4. Selecionar o pedido prioritário.

5. Atualizar a fila em caso de mudanças ou cancelamentos.


*“Nossa solução separa a importância do pedido da urgência do prazo.*


*A inteligência artificial analisa fatores como distância, SLA, valor do produto e reputação do vendedor para gerar uma pontuação de prioridade de zero a cem.*


*Já a urgência é calculada por uma regra matemática: quanto menos tempo falta para o prazo, maior a pontuação de urgência.*


*Depois, combinamos os dois resultados, atribuindo 70% de peso à prioridade da IA e 30% à urgência. O Heap organiza os pedidos pela pontuação final, permitindo consultar rapidamente qual deve ser considerado primeiro.*


*Esses pesos são uma proposta inicial. Precisamos testar a estratégia com dados reais para verificar se ela realmente reduz atrasos e melhora a eficiência logística“*


**3\. Diagrama**


**Fluxo de funcionamento:**


Receber pedido


↓


Calcular prioridade e urgência


↓


Inserir ou atualizar no Heap


↓


Selecionar pedido prioritário


↓


Verificar prazo e condições operacionais


↓


Encaminhar para expedição


↓


Atualizar a fila e repetir o processo.


O diagrama representa a entrada, a organização, a atualização e o processamento dos pedidos.


**4\. Trade-offs**


**Vantagens**


1. Consulta rápida do pedido prioritário.

2. Atualização eficiente quando novos pedidos chegam.

3. Considera tanto a importância quanto a urgência.


**Desvantagens**


1. Exige regras claras para calcular as prioridades.

2. Os pesos precisam ser testados e ajustados.

3. Pode deixar pedidos esperando demais se a prioridade não for bem equilibrada.


**Justificativa:** o Heap foi escolhido porque permite identificar rapidamente o próximo pedido, sem precisar ordenar toda a lista novamente a cada alteração.


O Insertion Sort e o Selection Sort apresentam complexidade O(n²), o que pode comprometer o desempenho com grandes volumes de pedidos. Já o Merge Sort e o Quick Sort são mais eficientes na ordenação de listas completas, mas menos adequados para atualizações frequentes.


Por isso, a fila de prioridade baseada em Heap seria a melhor escolha, pois permite consultar o pedido mais prioritário em O(1) e realizar inserções e remoções em O(log n), e reordenação.


**5\. Próximos passos**


* Comparar a solução com uma fila simples por ordem de chegada.

* Medir o atraso médio, os pedidos processados por hora e o percentual de pedidos dentro do prazo.

* Simular novos pedidos, cancelamentos e alterações de prazo.

* Ajustar os pesos da pontuação com base nos resultados obtidos.


**Sugestão de pseudocódigo:**

Colocarei duas sugestões: uma será o pseudocódigo completo e outra, compacto, para a apresentação. OBS: Usei o claude para refinar o código.

**Versão completa:**

```text
CONSTANTES
    PESO_IA       = 0.7
    PESO_URGENCIA = 0.3
    HORIZONTE     = 120                     // minutos de referência
    ESPACO        = { P: 1, M: 2, G: 4 }    // espaço de cada tamanho na doca
    CAPACIDADE    = 20                      // espaço total da doca (valor de teste)

VARIÁVEIS
    heap        = Heap máximo               // o maior valor de "pontuacao" fica no topo
    espacoLivre = CAPACIDADE

// ---------- 1. Cálculos ----------

FUNÇÃO calcularUrgencia(minutosRestantes)
    urgencia = (HORIZONTE - minutosRestantes) / HORIZONTE * 100
    RETORNA máximo(0, mínimo(100, urgencia))  // limita entre 0 e 100

FUNÇÃO calcularPontuacao(pedido)
    urgencia = calcularUrgencia(pedido.dispatchWindow)
    RETORNA PESO_IA * pedido.priorityScore
             + PESO_URGENCIA * urgencia

// ---------- 2. Entrada de pedidos ----------

PROCEDIMENTO receberPedido(pedido)
    pedido.cancelado = FALSO
    pedido.pontuacao = calcularPontuacao(pedido)
    heap.inserir(pedido)  // O(log n)

// ---------- 3. Seleção do próximo pedido ----------

FUNÇÃO selecionarPedido()
    adiados = lista vazia

    ENQUANTO heap não estiver vazio FAÇA
        pedido = heap.removerTopo()  // O(log n)

        SE pedido.cancelado ENTÃO
            CONTINUE  // ignora pedidos cancelados

        SE espacoLivre >= ESPACO[pedido.sizeCategory] ENTÃO
            espacoLivre = espacoLivre - ESPACO[pedido.sizeCategory]

            PARA CADA pedidoAdiado EM adiados FAÇA
                heap.inserir(pedidoAdiado)

            RETORNA pedido  // este vai para embalagem
        SENÃO
            adiados.adicionar(pedido)  // não cabe agora; tenta o próximo

    PARA CADA pedidoAdiado EM adiados FAÇA
        heap.inserir(pedidoAdiado)

    RETORNA NULO  // doca cheia; aguardar

// ---------- 4. Mudanças e cancelamentos ----------

PROCEDIMENTO cancelarPedido(pedido)
    pedido.cancelado = VERDADEIRO
    // remoção preguiçosa: sai quando chegar ao topo

PROCEDIMENTO atualizarPedido(pedido, novoPriorityScore)
    cancelarPedido(pedido)  // invalida a versão antiga
    novo = copia(pedido)
    novo.priorityScore = novoPriorityScore
    receberPedido(novo)  // entra com a pontuação nova

PROCEDIMENTO concluirEmbalagem(pedido)
    espacoLivre = espacoLivre + ESPACO[pedido.sizeCategory]
    // libera o espaço ocupado na doca

// ---------- 5. Repriorização com o passar do tempo ----------

PROCEDIMENTO recalcularFila()  // roda a cada 60 segundos
    PARA CADA pedido EM heap FAÇA
        pedido.dispatchWindow = minutosAteExpirar(pedido)
        pedido.pontuacao = calcularPontuacao(pedido)

    heap.reconstruir()  // O(n)

// ---------- 6. Ciclo principal ----------

ENQUANTO sistema estiver ativo FAÇA
    SE chegou novo pedido ENTÃO
        receberPedido(pedido)

    SE pedido foi cancelado ENTÃO
        cancelarPedido(pedido)

    SE pedido foi alterado ENTÃO
        atualizarPedido(pedido, novoScore)

    SE doca liberou espaço ENTÃO
        concluirEmbalagem(pedido)

    SE passaram 60 segundos ENTÃO
        recalcularFila()

    proximo = selecionarPedido()

    SE proximo != NULO ENTÃO
        enviarParaEmbalagem(proximo)
```

**Versão para slide:**

```text
Para cada pedido recebido:
    urgencia = máximo(0, mínimo(100, (120 - dispatchWindow) / 120 * 100))
    pontuacao = 0,7 * priorityScore + 0,3 * urgencia
    inserir pedido no Heap  // maior pontuação fica no topo

Quando a doca tiver espaço:
    pedido = topo do Heap

    SE sizeCategory couber na doca ENTÃO
        enviar para embalagem
    SENÃO
        tentar o próximo da fila

Se o pedido for cancelado ou alterado:
    invalidar a versão antiga
    reinserir com a pontuação nova

A cada minuto:
    atualizar dispatchWindow de todos os pedidos
    recalcular a urgência
    reorganizar o Heap
```
