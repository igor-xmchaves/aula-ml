\# Versionamento de Dados e Modelos com Git e DVC



\## Atividade Prática 07



\- \*\*Universidade:\*\* Universidade Federal do Ceará (UFC)

\- \*\*Disciplina:\*\* Engenharia de Sistemas Inteligentes (CK0444)

\- \*\*Professor:\*\* Lincoln S. Rocha



\## Objetivo



Versionar datasets, partições e modelos utilizando Git e DVC, avaliando o impacto da correção de um erro de rotulagem em um classificador de chamados comuns e urgentes.



\## Pré-requisitos



\- Git;

\- Python 3.10 ou superior;

\- DVC 3.x;

\- Acesso ao repositório GitHub.



Para instalar o DVC:



```bash

pip install "dvc>=3,<4"

```



\## Armazenamento DVC



O armazenamento dos datasets e modelos está configurado no diretório local `../dvc-storage`, localizado no mesmo nível do repositório.



Para consultar a configuração:



```bash

dvc remote list

```



O armazenamento deve conter os artefatos previamente enviados com `dvc push`.



\## Versões registradas



| Tag | Descrição |

|---|---|

| dados-v1 | Dataset original com erro de rotulagem. |

| modelo-r1 | Modelo treinado com o dataset original. |

| dados-v2 | Dataset com o rótulo do chamado 006 corrigido. |

| modelo-r2 | Modelo treinado com o dataset corrigido. |



\## Restauração do modelo r1



Em um diretório que contenha o armazenamento `dvc-storage`, execute:



```bash

git clone https://github.com/igor-xmchaves/aula-ml.git aula-ml-restauracao

cd aula-ml-restauracao

git switch --detach modelo-r1

dvc pull

```



Após a restauração, os hashes SHA-256 dos artefatos devem ser comparados com os registrados em `reports/modelo.json`.



Para restaurar a segunda versão:



```bash

git switch --detach modelo-r2

dvc pull

```



A tag `modelo-r2` deve estar publicada no GitHub.



\## Resultados



| Métrica | Modelo r1 | Modelo r2 |

|---|---:|---:|

| Acurácia | 75% | 100% |

| Recall de comuns | 100% | 100% |

| Recall de urgentes | 50% | 100% |



A correção do rótulo melhorou o reconhecimento dos chamados urgentes sem prejudicar a classificação dos chamados comuns.



O relatório detalhado está disponível em `reports/comparacao.md`.

