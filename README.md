<div align="center">

<img src="assets/images/veloxmart-banner.png" alt="VeloxMart — Marketplace Priority Sorter Banner" width="100%" />

# 📦 VelozMart — Marketplace Priority Sorter (MPS)

**Proposta Técnica de Priorização de Pedidos em Tempo Real e Alocação Física de Doca**  
*Projeto Final do Coding Tank — Programa **DiverseDEV 2026** (Ada Tech & Mercado Eletrônico)*

</div>

---

## 🎯 Sobre o Projeto

Este repositório contém a solução conceitual e arquitetural desenvolvida para o desafio **Marketplace Priority Sorter (MPS)** da **VelozMart**. O objetivo é organizar milhares de pedidos aguardando expedição em tempo real para **minimizar atrasos (quebras de SLA)** e **otimizar o uso do espaço físico da doca de embalagem**, considerando:

* **`priorityScore` (`0–100`):** Nota de relevância calculada por IA (distância, SLA, valor do item e reputação do vendedor).
* **`dispatchWindow` (minutos):** Tempo restante até o prazo de expedição expirar.
* **`sizeCategory` (`P`, `M`, `G`):** Volume físico do pacote que ocupa vagas na bancada (`P = 1 vaga`, `M = 2 vagas`, `G = 4 vagas`).

---

## 🧠 Resumo da Solução (Arquitetura Híbrida)

Nossa proposta combina duas estruturas clássicas para unir velocidade de processamento e aproveitamento físico da doca:

1. **Estágio 1 — Triagem Global com `Max-Heap` (`O(log n)`):**
   * Mantém o pedido mais urgente/importante sempre no topo em tempo logarítmico, sem precisar reordenar toda a lista a cada chegada.
   * **Pontuação Composta:** `70% Nota da IA + 30% Urgência do Prazo` (janela de 120 min), somada a um **Bônus Crítico de SLA (+25 pontos)** quando restam `≤ 15 minutos`.
   * **Manutenção Dinâmica:** Remoção preguiçosa (*Lazy Deletion* em `O(1)`) para cancelamentos/atualizações e reconstrução periódica via `Heapify` (`O(n)`) a cada 60 segundos.
2. **Estágio 2 — Buffer de Doca com `Insertion Sort` (`O(k)`, onde `k = 10`):**
   * Abastece um lote curto na bancada com os 10 pedidos mais prioritários do Heap.
   * Caso o 1º pedido seja Grande (`G`) e não caiba na doca naquele segundo, despacha imediatamente o próximo pacote Pequeno (`P`) ou Médio (`M`) do buffer, evitando travar a operação.

---

## 📂 Estrutura do Repositório

```text
DiverseDev/
├── entrega_velozmart_mps.html   # Entrega final interativa (Proposta Técnica + Roteiro de Fala + Exportação PDF)
├── README.md                    # Documentação principal do repositório
├── AGENT.md                     # Contexto do projeto e instruções para Agentes de IA e colaboradores
├── LICENSE                      # Licença MIT
├── .gitignore                   # Arquivos ignorados pelo Git
│
├── docs/                        # Documentos originais, rascunhos e materiais de referência
│   ├── enunciado-projeto.md     # Enunciado original do desafio (Projeto Divesedev.md)
│   ├── brainstorming-grupo.md   # Anotações do grupo e versões do pseudocódigo (ideias do grupo.md)
│   ├── guia-coding-tank.html    # Guia interativo original do Coding Tank (projeto_final_mps.html)
│   ├── apresentacao/
│   │   └── Apresentacao-Corporate-Heap-Priorizacao-Canva.pdf   # Slides da apresentação
│   └── materiais-aula/
│       ├── Aula-Dia-01.pdf      # Material da Aula 1
│       └── Big-O-Didatico.pdf   # Guia didático sobre complexidade Big-O
│
└── assets/
    └── images/                  # Identidade visual (Logos e Banners VeloxMart / DiverseDEV)
        ├── veloxmart-banner.png
        ├── veloxmart-logo.png
        └── diversedev-hero.png
```

---

## 🚀 Como Visualizar e Editar

1. **Visualizar a Proposta / Gerar PDF:**
   * Basta abrir o arquivo [`entrega_velozmart_mps.html`](entrega_velozmart_mps.html) em qualquer navegador.
   * Use o botão **"🎙️ Mostrar / Ocultar Roteiro de Fala"** no topo da página para ver as falas sugeridas para os 5 integrantes.
   * Use o botão **"🖨️ Imprimir / Salvar como PDF Oficial"** para exportar o documento pronto para entrega.
2. **Editar o Projeto:**
   * Todo o conteúdo, estilo e roteiro da entrega final está centralizado em [`entrega_velozmart_mps.html`](entrega_velozmart_mps.html), facilitando a edição direta em qualquer editor de texto (como o VS Code) sem necessidade de instalar dependências.
