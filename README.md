yhg´[tp-0o=erfdd=================================================================================================================================================================================================ol-gfv4p´jjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjjj<h1> Projeto Ciencia de Dados - Análise de Turismo Global</h1>

<hr>
<br>

<h1>1. Introdução</h1>
Tem como objetivo analisar o turismo global. A análise foca em três principais aspectos:

<b>Turismo Global:</b> Evolução das chegadas de turistas e receitas por país.

<b>Turismo e Economia:</b> Relação entre turismo e indicadores econômicos, como PIB, inflação e desemprego.

<b>Gastos e Movimentação:</b> Análise dos gastos com turismo e dos principais países emissores de turistas.

<b>Tendências e Crescimento:</b> Identificação de tendências e crescimento do turismo ao longo dos anos.

<hr>
<br>

<h1>2. Tecnologias Utilizadas</h1>

Linguagem: Python

Bibliotecas:

streamlit: Para criar a interface do dashboard.

pandas: Para manipulação e análise dos dados.

plotly.express: Para visualização dos dados de forma interativa.

3. Fonte dos Dados

Os dados foram obtidos do arquivo world_tourism_economy_data.csv. As principais colunas utilizadas incluem:

country: Nome do país.

year: Ano da observação.

tourism_arrivals: Número de chegadas de turistas.

tourism_receipts: Receita gerada pelo turismo.

tourism_exports: Exportações relacionadas ao turismo.

tourism_departures: Saídas de turistas.

tourism_expenditures: Gastos com turismo.

gdp: PIB do país.

inflation: Índice de inflação.

unemployment: Taxa de desemprego.

4. Processo de ETL (Extração, Transformação e Carga)

Antes de realizar as análises, os dados passam por um tratamento que inclui:

Carregamento dos Dados:

O arquivo CSV é carregado em um DataFrame Pandas.

Limpeza e Tratamento:

Remoção de valores ausentes nas colunas essenciais.

Cálculo da contribuição do turismo no PIB (tourism_contribution_gdp).

Criação de Novas Métricas:

tourism_contribution_gdp: Percentual da receita do turismo em relação ao PIB.

gdp_growth: Crescimento percentual do PIB.

rolling_mean: Média móvel do turismo para suavizar variações anuais.

5. Estrutura do Dashboard

O dashboard é dividido em quatro páginas, acessíveis pelo menu lateral:

5.1 Turismo Global

Foca na análise geral do turismo mundial.

Gráfico 1: Evolução das chegadas de turistas ao longo dos anos (linha).

Gráfico 2: Top 10 países com mais turistas (barras).

Gráfico 3: Top 10 países com maior receita de turismo (barras).

5.2 Turismo e Economia

Explora a relação entre turismo e indicadores econômicos.

Gráfico 1: Relação entre PIB e receita do turismo (dispersão).

Gráfico 2: Impacto da inflação na receita do turismo (dispersão).

Gráfico 3: Correlação entre turismo e desemprego (dispersão).

5.3 Gastos e Movimentação

Analisa os gastos e fluxos de turistas entre os países.

Gráfico 1: Relação entre exportações e gastos com turismo (dispersão).

Gráfico 2: Top 10 países emissores de turistas (barras).

Gráfico 3: Comparação entre turismo receptivo e emissivo (dispersão).

5.4 Tendências e Crescimento

Identifica tendências e padrões de crescimento do turismo.

Gráfico 1: Crescimento percentual do turismo ao longo dos anos (linha).

Gráfico 2: Média móvel de turismo por país (linha).

Gráfico 3: Relação entre crescimento do PIB e turismo (dispersão).

6. Como Executar o Projeto

Para rodar o dashboard, siga os passos abaixo:

Instale as dependências:

pip install streamlit pandas plotly

Salve o código Python do dashboard em um arquivo app.py.

Execute o comando:

streamlit run app.py

Acesse o dashboard pelo navegador no link fornecido pelo Streamlit.

7. Considerações Finais

Este projeto fornece insights sobre o impacto do turismo na economia global, facilitando a tomada de decisões para governos e empresas do setor. Ele pode ser expandido com novas métricas e previsões baseadas em modelos de Machine Learning.

Se precisar de melhorias ou novos gráficos, basta ajustar o código no arquivo principal do Streamlit!
