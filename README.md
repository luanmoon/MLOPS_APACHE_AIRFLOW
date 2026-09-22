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

## Arquitetura do Pipeline (DAG)

* **extract_task:** Lê o dataset de séries temporais bruto (Captura_52.csv), isolando os dados e convertendo-os para o formato serializado JSON para tráfego seguro via XCom do Airflow.

* **transform_task:** Aplica técnicas avançadas em duas fases:

* **Seleção de Features:** Utiliza uma janela deslizante (Sliding Window), cálculo de Z-Score e memória com atenuação (Fading Memory) para filtrar e selecionar as colunas mais informativas de forma dinâmica.

* **Engenharia de Recursos Temporais:** Gera estatísticas móveis (Rolling Mean/Std, Expanding Mean), estabilização de variância via Box-Cox, decomposição de tendência/sazonalidade e análise no domínio da frequência via Transformada Rápida de Fourier (FFT).

* **load_task:** Persiste o resultado final consolidando as novas variáveis em um arquivo limpo e estruturado (features.csv).
---

## Como executar o projeto
### Pré-requisitos:
Docker e Docker Compose instalados e em execução na máquina.

### Tutorial

Clone este repositório na sua máquina:

  ```text(
   git clone [https://github.com/SEU_USUARIO/MLOPS_APACHE_AIRFLOW.git](https://github.com/SEU_USUARIO/MLOPS_APACHE_AIRFLOW.git)
   cd MLOPS_APACHE_AIRFLOW
```
Certifique-se de que o arquivo .env está configurado com o seu UID e as dependências extras de bibliotecas estatísticas:
```text
AIRFLOW_UID=50000
_PIP_ADDITIONAL_REQUIREMENTS=scipy statsmodels

```
Inicialize os containers do Docker Compose em segundo plano:

```
docker compose up airflow-init
docker compose up -d

```

Acesse a interface web do Airflow no navegador:

URL: http://localhost:8080

Usuário: airflow

Senha: airflow

Ative a DAG pipeline_feature_engineering e clique no botão de execução (Trigger DAG). O arquivo features.csv será gerado automaticamente na pasta data/.

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

´´
