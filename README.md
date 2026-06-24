# GMI_Incibatorio

# 📊 Painel de Controle e Análise de Incubatórios (Hatchery Analytics)

Este projeto consiste em um dashboard analítico focado no monitoramento e otimização dos indicadores de eclosão e eficiência de incubatórios, comparando dados **Reais vs. Padrão (Metas)** para os anos de 2025 e 2026.

---

## 🗺️ Estrutura de Navegação (Sidebar)

O painel é segmentado nas seguintes visões dinâmicas:
- **Eficiência de Eclosão** (Visão Geral & Histórico)
- **Participação de Região** (Análise Geográfica)
- **Participação de Linhagem** (Análise Genética)
- **Faixa Etária** (Idade da Ave)
- **Tipo de Ovo** (Classificação)
- **Dias de Estoque** (Impacto do armazenamento)
- **Incubatórios** (Performance por Unidade)
- **Impacto Formação** & **Ovoscopia**

---

## 🧮 Regras de Negócio & Fórmulas de Cálculo

Os indicadores do painel utilizam as seguintes bases matemáticas para as comparações nos gráficos:

### 1. Eficiência de Eclosão e Padrão
* **Eficiência de Eclosão (%):**
  $$\text{Eficiência de Eclosão} = \left( \frac{\text{Eclosão}}{\text{Eclosão Pdr}} \right) \times 100$$
* **Padrão Eficiência (%):**
  $$\text{Padrão Eficiência} = \left( \frac{\text{Efic. Eclo. Pdr}}{\text{Eclosão Pdr}} \right) \times 100$$

### 2. Eclosão Real vs. Padrão
* **Eclosão Real (%):**
  $$\text{Eclosão Real} = \left( \frac{\text{Eclosão}}{\text{Ovos Incub.}} \right) \times 100$$
* **Padrão Eclosão (%):**
  $$\text{Padrão Eclosão} = \left( \frac{\text{Eclosão Pdr}}{\text{Ovos Incub.}} \right) \times 100$$

### 3. Impacto de Pintos (Volume)
$$\text{Impacto de Pintos} = \text{Eclosão Pdr} - \text{Eclosão}$$

### 4. Dias de Estoque Médio
$$\text{Dias de Estoque Médio} = \frac{\sum (\text{Ovos Incubados} \times \text{Dias Estoque})}{\text{TOTAL Ovos Incubados}}$$

### 5. Volume de Ovos Incubados (%)
$$\%\text{ Volume de Ovos Incubados} = \left( \frac{\text{Ovos Incubados}}{\text{TOTAL Ovos Incubados}} \right) \times 100$$

---

## 🖥️ Matriz de Telas, Gráficos e Métricas

Abaixo está o mapeamento mínimo de componentes visuais necessários para cada seção do painel:

| Seção (Sidebar) | Visualizações / Gráficos Requeridos | Fórmulas Aplicadas |
| :--- | :--- | :--- |
| **Eficiência de Eclosão** | • Gráfico de Linha: Histórico Temporal por Mês (2025 vs. 2026 vs. Meta)<br>• Tabela de dados analítica de apoio | Fórmulas 1 e 2 |
| **Participação de Região** | • Gráfico de Barras: Unidades por % de Eficiência<br>• Gráfico de Pizza: % de Volume de Ovos Incubados<br>• Tabela de dados inferior | Fórmulas 1, 2 e 5 |
| **Participação de Linhagem**| • Gráfico de Barras: % de Eficiência por Linhagem/Raça<br>• Gráfico de Pizza: % de Volume de Ovos por Linhagem<br>• Gráfico de Barras: Impacto por Linhagem/Raça<br>• Tabela de dados de apoio | Fórmulas 1, 3 e 5 |
| **Faixa Etária** | • Gráfico de Barras: % de Eficiência por Faixa/Raça<br>• Gráfico de Pizza: % de Volume de Ovos<br>• Gráfico de Barras: Impacto por Faixa Etária<br>• Tabela de dados detalhada | Fórmulas 1, 3 e 5 |
| **Tipo de Ovo** | • Gráfico de Barras: % de Eficiência por Tipo de Ovo<br>• Gráfico de Pizza: % de Volume por Tipo<br>• Gráfico de Barras: Impacto por Tipo de Ovo<br>• Tabela de dados de apoio | Fórmulas 1, 3 e 5 |
| **Dias de Estoque** | • Gráfico de Barras: % de Ovos Incubados por Dia de Estoque<br>• Gráfico de Linha: Histórico Temporal por Mês (2025 vs. 2026) | Fórmulas 4 e 5 |
| **Incubatórios** | • Gráfico Combinado (Barras + Linha): Barras para Eclosão Real x Padrão por Incubatório, e Linha sobreposta para Eficiência de Eclosão | Fórmulas 1 e 2 |

---

## 📖 Dicionário de Dados (`.xlsx`)

Mapeamento de colunas da base de dados original para referência no desenvolvimento do modelo:

* **Dados de Identificação e Origem:**
  * `Incubatório`: Nome do Incubatório correspondente.
  * `Unidade Granja`: Região de localização dos lotes.
  * `Granja`: Nome/Identificador da granja de produção.
  * `Lote`: Código do lote de produção.
* **Características Biológicas:**
  * `Raça Ave`: Grupo genético / Linhagem agrupada.
  * `Linhagem`: Nome completo da linhagem da ave.
  * `Faixa Idade`: Classificação da faixa etária da ave.
  * `Sem`: Idade exata da ave em semanas.
  * `Tp. Ovo`: Descrição do tipo de ovo incubado.
* **Logística e Produção:**
  * `Dt Nasc.`: Data de nascimento do pintinho (referente ao ciclo de incubação).
  * `Dias Estoq.`: Dias de armazenamento/estoque do ovo antes de incubar.
  * `Ovos Incub.`: Quantidade total de ovos colocados em incubação.
* **Qualidade e Resultados:**
  * `Contam.`: Quantidade de ovos identificados como contaminados.
  * `Vend.`: Quantidade de pintos nascidos considerados vendáveis.
  * `Elim.`: Quantidade de pintos que precisaram ser eliminados.
  * `Eclosão`: Volume total de nascimentos vivos (`Vendáveis` + `Eliminados`).
* **Metas e Referências:**
  * `Eclosão Pdr`: Volume estimado de nascimentos baseando-se no padrão esperado.
  * `Efic. Eclo. Pdr`: Meta/Padrão volumétrico estabelecido na etapa de Planejamento.