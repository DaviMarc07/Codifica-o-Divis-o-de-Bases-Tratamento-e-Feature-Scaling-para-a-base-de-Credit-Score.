# Preparação Final para Modelagem de Credit Score

1. Visão Geral do Projeto
Este projeto consiste na fase crucial de Preparação Final dos Dados antes da aplicação dos algoritmos de Machine Learning. O objetivo é transformar a base de dados de Credit Score (que contém features categóricas e desbalanceamento de classes) em um formato totalmente numérico e escalado, pronto para o treinamento.

As etapas principais incluem: Codificação, Divisão de Bases, Balanceamento de Classes (SMOTE) e Feature Scaling.

2. Carregamento e Codificação Inicial
Esta seção trata do carregamento da base e da conversão inicial das variáveis categóricas.

Importação de Bibliotecas: Além das bibliotecas padrão (pandas, numpy, matplotlib, seaborn), foram importadas ferramentas essenciais de pré-processamento e balanceamento: train_test_split, SMOTE (da imblearn) e LabelEncoder.

Carregamento e Padronização: O arquivo CREDIT_SCORE_PROJETO_PARTE1.csv é carregado, e os nomes das colunas são padronizados para snake_case.

Codificação da Variável Alvo (Credit Score):

Método Escolhido: LabelEncoder.

Justificativa: A variável alvo (Credit Score) possui categorias ordenadas (Low, Average, High). O LabelEncoder é usado para atribuir valores numéricos ordinais (0, 1, 2), mantendo a ordem sem criar muitas colunas dummy, o que é apropriado para a classificação multi-classe.

3. Divisão de Bases (Treino e Teste)
Antes de qualquer manipulação que possa vazar informações da base de teste, o dataset é dividido.

Método Escolhido: train_test_split.

Proporção: A divisão padrão de 70% para Treino e 30% para Teste é utilizada.

Justificativa: A separação garante que o modelo seja avaliado em dados que ele nunca viu, medindo sua verdadeira capacidade de generalização e evitando overfitting.

4. Tratamento do Desbalanceamento de Classes (SMOTE)
A variável alvo original (Credit Score) mostrou-se desbalanceada, com a classe High dominando a base.

Problema: Um modelo treinado em dados desbalanceados prioriza a classe majoritária, resultando em baixa performance e alta taxa de erros na previsão das classes minoritárias (Low e Average).

Método Escolhido: SMOTE (Synthetic Minority Over-sampling Technique).

Processo: O SMOTE cria amostras sintéticas para as classes minoritárias na base de treino, até que todas as classes atinjam o mesmo número de observações da classe majoritária.

Aplicação: O SMOTE é aplicado APENAS na base de treino (X_train e y_train) para evitar o vazamento de dados (data leakage) para a base de teste.

Verificação: O código mostra claramente o gráfico e a contagem do target balanceado, onde todas as classes passam a ter um número igual de amostras.

5. Feature Scaling (Padronização - StandardScaler)Esta etapa final de pré-processamento trata as variáveis numéricas para que elas tenham escalas comparáveis.Método Escolhido: StandardScaler.Processo: O StandardScaler transforma os dados para que tenham média ($\mu$) zero e desvio padrão ($\sigma$) um. $$Z = \frac{x - \mu}{\sigma}$$

ustificativa: A padronização é essencial para algoritmos baseados em distância (como K-NN) ou gradiente (como Regressão Logística) e evita que features com grandes magnitudes (ex: renda_anual em milhares) dominem o cálculo da distância ou do custo, em detrimento de features com pequenas magnitudes (ex: idade).

Aplicação: O StandardScaler é treinado (fit) apenas na base de treino e então aplicado (transform) nas bases de treino e teste.

6. Conclusão da Preparação
Ao final, as bases de treino (X_train_balanceado, y_train_balanceado) e de teste (X_test, y_test) estão:

Com variáveis categóricas codificadas.

Com o target na base de treino balanceado (graças ao SMOTE).

Com variáveis numéricas escaladas (graças ao StandardScaler).

