# 🤖 AGENT.md — Guia para Agentes de IA e Colaboradores

Este arquivo orienta assistentes de IA e pessoas colaboradoras sobre como o projeto **VelozMart — Marketplace Priority Sorter (MPS)** está organizado e como editá-lo mantendo a simplicidade e consistência.

---

## 1. Contexto do Projeto

* **Programa:** Coding Tank — DiverseDEV 2026 (Ada Tech & Mercado Eletrônico).
* **Natureza do Projeto:** Protótipo conceitual e proposta técnica de engenharia (TI → Logística) para priorização de pedidos em tempo real.
* **Regra da Solução:** Arquitetura híbrida em 2 estágios combinando **Max-Heap (`O(log n)`)** com pontuação composta (`70% IA + 30% Urgência + Bônus Crítico de +25 pts para prazo <= 15 min`) e um **Buffer de Doca (`k = 10`) ordenado com Insertion Sort (`O(k)`)** para encaixar pacotes `P`, `M` e `G` conforme as vagas livres da bancada.

---

## 2. Onde Editar Cada Coisa

O projeto foi mantido intencionalmente simples e sem dependências externas:

* **[`entrega_velozmart_mps.html`](entrega_velozmart_mps.html):**
  * É o arquivo principal do projeto. Contém toda a estrutura HTML, estilização CSS (tema corporativo escuro/laranja VelozMart + regras `@media print`) e o botão de alternância do roteiro de apresentação.
  * **Seções Obrigatórias:** (1) Problema, (2) Algoritmo/Estrutura, (3) Diagrama Visual, (4) Trade-offs & Big-O, (5) Métricas & Próximos Passos.
  * **Roteiro de Apresentação:** Fica dentro das `<div>` com a classe `.speaker-cue` no início de cada seção.
* **[`docs/enunciado-projeto.md`](docs/enunciado-projeto.md) e [`docs/guia-coding-tank.html`](docs/guia-coding-tank.html):**
  * Contêm as instruções originais e os requisitos mínimos da avaliação. Não devem ter suas regras alteradas.
* **[`docs/brainstorming-grupo.md`](docs/brainstorming-grupo.md):**
  * Rascunho colaborativo com as ideias originais do grupo e as duas versões de pseudocódigo (completa e compacta para slide).

---

## 3. Boas Práticas ao Modificar o `entrega_velozmart_mps.html`

1. **Mantenha o arquivo autocontido:** Evite adicionar bibliotecas externas que precisem de `npm` ou build, para que qualquer pessoa do grupo consiga abrir o `entrega_velozmart_mps.html` com duplo-clique em qualquer computador.
2. **Preserve a Acessibilidade:** As tags de status utilizam **Símbolo + Cor de Alto Contraste + Texto** (`● Alerta SLA`, `▲ Alta Prioridade`, `◆ Buffer de Doca`, `✓ Expedido`) para não depender apenas de cores.
3. **Preserve a Impressão PDF (`@media print`):** Garanta que a barra superior (`.top-bar`) continue oculta na impressão e que os cards (`.card`) mantenham `break-inside: avoid`.
