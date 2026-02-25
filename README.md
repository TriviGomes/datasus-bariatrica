# 🏥 DATASUS Bariátrica — MedTech Analytics

> **Workshop de Dados em Saúde** | Inteligência de mercado com dados públicos do SUS

Extração e análise de cirurgias bariátricas financiadas pelo SUS (2022–2024),  
com geração de CSVs prontos para dashboards no **Power BI**.

---

## 🎯 Caso de Uso

Uma empresa de **MedTech** precisa entender o mercado público de cirurgia bariátrica para:

- 📍 Identificar **regiões subatendidas** e oportunidades de expansão
- 🏨 Mapear **hospitais líderes** em volume (potenciais clientes/parceiros)
- 👤 Entender o **perfil dos pacientes** do SUS
- 📈 Analisar a **tendência temporal** do mercado público
- 💰 Benchmarkar o **valor pago pelo SUS** por procedimento

---

## 🚀 Como Usar no GitHub Codespaces

**1. Abra o repositório no Codespaces:**

[![Abrir no Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/)

Clique em **Code → Codespaces → Create codespace on main**.  
O ambiente Python será configurado automaticamente (pode levar ~2 min).

**2. Opção A — Notebook interativo (recomendado para o workshop):**

```bash
jupyter notebook analise_bariatrica.ipynb
```

**3. Opção B — Script direto (extração completa):**

```bash
python scripts/extrair_bariatrica.py
```

**4. Os CSVs serão gerados em `/output/` — baixe e importe no Power BI.**

---

## 📁 Estrutura do Projeto

```
datasus-bariatrica/
│
├── .devcontainer/
│   └── devcontainer.json        # Config do GitHub Codespaces
│
├── scripts/
│   └── extrair_bariatrica.py    # Script de extração completo
│
├── output/                      # CSVs gerados (não versionados)
│
├── analise_bariatrica.ipynb     # Notebook interativo passo a passo
├── requirements.txt             # Dependências Python
├── .gitignore
└── README.md
```

---

## 📊 Arquivos Gerados

| Arquivo | Descrição | Uso no Power BI |
|---|---|---|
| `bariatrica_sus_2022_2024.csv` | Base completa (1 linha = 1 internação) | Tabela principal com drill-through |
| `resumo_por_uf_ano.csv` | Volume e valor por estado e ano | Mapa do Brasil + gráfico de barras |
| `resumo_por_procedimento.csv` | Mix de tipos de cirurgia | Gráfico de rosca / treemap |
| `perfil_demografico.csv` | Distribuição por sexo, idade e raça | Pirâmide etária |
| `top_hospitais.csv` | 20 hospitais com maior volume | Tabela de oportunidades comerciais |

---

## 🔬 Procedimentos Extraídos (Códigos SIGTAP)

| Código | Procedimento |
|---|---|
| 0407010090 | Bypass Gástrico com Derivação Intestinal (Y-de-Roux) |
| 0407010120 | Gastrectomia Vertical (Sleeve) |
| 0407010031 | Bandagem Gástrica Ajustável |
| 0407010065 | Derivação Biliopancreática |

---

## 🔧 Configurações Disponíveis

No início de `scripts/extrair_bariatrica.py` ou no notebook, você pode ajustar:

```python
ANOS = [2022, 2023, 2024]   # período de extração

UFS = ['SP', 'RJ', 'MG']   # para testes rápidos
# ou todos os 27 estados para extração completa
```

---

## 📥 Importando no Power BI

1. Abra o Power BI Desktop
2. **Obter Dados → Texto/CSV**
3. Selecione o arquivo desejado da pasta `/output/`
4. Defina o separador como **ponto e vírgula (`;`)**
5. Encoding: **UTF-8**

> 💡 **Dica:** O campo `COD_CNES_HOSPITAL` pode ser cruzado com o  
> [CNES online](https://cnes.datasus.gov.br/) para enriquecer com nome e endereço do hospital.

---

## 📦 Dependências

```
pysus>=0.12.0
pandas>=2.0.0
tqdm>=4.65.0
```

Instalação manual:
```bash
pip install -r requirements.txt
```

---

## 📚 Fontes de Dados

- **SIH/DATASUS** — Sistema de Informações Hospitalares do SUS  
  [datasus.saude.gov.br](https://datasus.saude.gov.br/)
- **SIGTAP** — Tabela de Procedimentos, Medicamentos e OPM do SUS  
  [sigtap.datasus.gov.br](http://sigtap.datasus.gov.br/)
- **PySUS** — Biblioteca Python para acesso ao DATASUS  
  [github.com/AlertaDengue/PySUS](https://github.com/AlertaDengue/PySUS)

---

## ⚠️ Avisos

- Os dados são públicos e de acesso irrestrito (Ministério da Saúde / DATASUS).
- A extração completa (27 UFs × 3 anos) pode levar **10–30 minutos** dependendo da conexão.
- Para workshops, recomenda-se extrair apenas 2–3 estados primeiro para validar o ambiente.
- Os arquivos `.dbc`/`.parquet` intermediários são excluídos automaticamente do versionamento.

---

*Desenvolvido para fins educacionais. Dados do Ministério da Saúde / DATASUS.*
