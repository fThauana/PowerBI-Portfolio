# 📊 Dashboard de Gestão de Service Desk (IT Help Desk)

![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-Analysis-blue?style=for-the-badge)
![Power Query](https://img.shields.io/badge/Power_Query-ETL-green?style=for-the-badge)

> **Status do Projeto:** Concluído ✅

---

## 🖼️ Visão Geral do Dashboard

![Print do Dashboard](dashboard_print.png)
*(Caso a imagem não carregue, consulte o arquivo PDF disponível neste repositório)*

---

## 💼 O Desafio de Negócio

Este projeto simula um cenário real de uma central de suporte de TI que precisava analisar **50.000 chamados**. O objetivo era transformar dados brutos em inteligência para responder a perguntas estratégicas:

1.  Qual é o volume total de tickets e como eles se dividem por categoria?
2.  A equipe está cumprindo o **SLA (Acordo de Nível de Serviço)** de 5 dias?
3.  Qual a severidade dos problemas que mais impactam o tempo de resolução?
4.  Existe diferença de prioridade no atendimento dependendo da senioridade do solicitante?

---

## 🛠️ Solução Técnica (Bastidores)

O projeto foi desenvolvido 100% no **Power BI Desktop**, passando por todas as etapas de um projeto de BI:

### 1. ETL e Tratamento de Dados (Power Query)
* **Limpeza:** Verificação de tipos de dados e renomeação de colunas técnicas (`FiledAgainst` → `Categoria`).
* **Regra de Negócio (Lógica Condicional):** Criação de uma coluna condicional para definir o Status do SLA.
    * *Lógica:* Se o chamado foi resolvido em até **5 dias**, considera-se "No Prazo". Caso contrário, "Atrasado".

### 2. Cálculos DAX (Medidas)
Não foram utilizadas colunas implícitas. Todas as métricas foram calculadas via medidas para garantir performance e escalabilidade:

* **Total de Chamados:** `COUNTROWS` da tabela fato.
* **Tempo Médio de Resolução:** `AVERAGE` da coluna de dias.
* **% de SLA Atingido:**
```dax
% SLA Atingido = 
VAR ChamadosNoPrazo = CALCULATE([Total Chamados], 'HelpDesk'[Status SLA] = "No Prazo")
RETURN
DIVIDE(ChamadosNoPrazo, [Total Chamados], 0)
```

### 3. Visualização de Dados (Storytelling)
O layout foi pensado para leitura rápida (Z-Pattern):
- KPIs (Cartões): Números macro no topo para visão imediata.
- Gráfico de Rosca: Para evidenciar a proporção de SLA (Vermelho vs. Azul).
- Gráfico de Barras: Ranking de categorias com maior demanda.
- Matriz: Detalhamento cruzando Severidade x Tempo Médio.
- Segmentação (Filtros): Interatividade para analisar por Senioridade (Junior, Regular, Management).

---

## 📂 Estrutura do Repositório
- ```IT_Help_Desk.pbix```: O arquivo editável do Power BI.
- ```dashboard_print.png```: Imagem estática do painel.
- ```dataset/```: Arquivo CSV original utilizado (Fonte: Kaggle).

---

## 🙋‍♀️ Autora
Thauana Vitoria Ferreira Farias

<a href="https://www.linkedin.com/in/thauana-vitoria-ferreira-farias" target="_blank">
    <img src="https://img.shields.io/badge/-LinkedIn-%230077B5?style=for-the-badge&logo=linkedin&logoColor=white" target="_blank">
  </a>
  
#

Este projeto foi desenvolvido para fins educacionais e de portfólio, demonstrando competências em Análise de Dados e Business Intelligence.


 
