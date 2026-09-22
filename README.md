# MLOPS_APACHE_AIRFLOW
# Pipeline de MLOps com Apache Airflow e Séries Temporais

Repositório desenvolvido para fins acadêmicos na disciplina de **MLOps**, com o objetivo de construir, orquestrar e automatizar um pipeline completo de engenharia de dados e extração de características (*Feature Engineering*) em um dataset de tráfego de rede (séries temporais), utilizando o **Apache Airflow** executado via **Docker**.

---

## Tecnologias Utilizadas

* **Orquestração:** Apache Airflow (TaskFlow API)
* **Containerização:** Docker & Docker Compose
* **Manipulação e Análise de Dados:** Python, Pandas, NumPy, SciPy
* **Estatística e Séries Temporais:** Statsmodels (Decomposição Sazonal), Transformada de Fourier (FFT), Box-Cox
* **Seleção de Features Online:** Algoritmo adaptado baseado no artigo **UFSSOD** (Streaming Feature Selection)

---

## Estrutura do Projeto

A organização dos diretórios segue os padrões de projetos de engenharia de dados e MLOps:

```text
MLOPS_APACHE_AIRFLOW/
├── dags/
│   ├── Captura_52.csv                # Dataset bruto de entrada
│   └── dag_feature_engineering.py    # Script principal contendo o DAG do Airflow
├── data/
│   └── features.csv                  # Dataset final processado com as features geradas
├── .env                              # Variáveis de ambiente e UID do Docker
└── docker-compose.yaml               # Configuração dos serviços do Airflow
