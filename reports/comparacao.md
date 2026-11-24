\# Relatório de Comparação — Modelos r1 e r2



\## 1. Alteração realizada



O dataset original apresentava um erro intencional de anotação no chamado de ID 006, referente a um bloqueio de acesso.



| Versão | ID | Texto | Classe |

|---|---|---|---|

| dados-v1 | 006 | bloqueio de acesso | comum |

| dados-v2 | 006 | bloqueio de acesso | urgente |



Apenas o rótulo desse exemplo de treinamento foi alterado. A partição de treino e teste, o algoritmo e os parâmetros foram mantidos.



\## 2. Comparação das métricas



| Métrica | Modelo r1 | Modelo r2 | Variação |

|---|---:|---:|---:|

| Acurácia | 75% | 100% | +25 p.p. |

| Recall de comuns | 100% | 100% | 0 p.p. |

| Recall de urgentes | 50% | 100% | +50 p.p. |

| Acertos | 3/4 | 4/4 | +1 |



\## 3. Análise dos resultados



O primeiro modelo associava incorretamente o token `bloqueio` à classe `comum`, causando um erro na classificação do chamado 010.



Após a correção do chamado 006 e o treinamento do modelo r2, o token `bloqueio` passou a ser associado à classe `urgente`.



Consequentemente, o recall dos chamados urgentes aumentou de 50% para 100%, enquanto o recall dos chamados comuns permaneceu em 100%.



\## 4. Evidências da restauração



A versão `modelo-r1` foi selecionada em um clone limpo do repositório. Os artefatos foram recuperados utilizando `dvc pull`, sem realizar um novo treinamento.



\### Hashes SHA-256 verificados



| Artefato | SHA-256 |

|---|---|

| data/chamados.csv | \[HASH DO DATASET] |

| data/split.csv | \[HASH DA PARTIÇÃO] |

| models/model.json | \[HASH DO MODELO] |



\*\*Commit restaurado:\*\* `\[SHA DO COMMIT]`



Os três hashes recuperados coincidiram com os valores registrados no manifesto original do modelo r1.



\## 5. Critério de aceitação



O modelo r2 deve melhorar o recall dos chamados urgentes sem reduzir o recall dos chamados comuns, utilizando a mesma partição de teste.



\## 6. Decisão



\*\*Modelo r2 aceito para este exercício.\*\*



A correção do erro de rotulagem melhorou a acurácia e o recall dos chamados urgentes, sem prejudicar o reconhecimento dos chamados comuns.



Entretanto, como o conjunto de teste possui apenas quatro exemplos, os resultados demonstram o efeito da correção neste exercício, não sendo suficientes para garantir a capacidade de generalização do modelo em um ambiente de produção.

