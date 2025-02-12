<h1> Projeto Ciencia de Dados - Análise de Turismo Global</h1>

<hr>
<br>

<h1>Introdução</h1>
Tem como objetivo analisar o turismo global. A análise foca em três principais aspectos:

<b>Turismo Global:</b> Evolução das chegadas de turistas e receitas por país.

<b>Turismo e Economia:</b> Relação entre turismo e indicadores econômicos, como PIB, inflação e desemprego.

<b>Gastos e Movimentação:</b> Análise dos gastos com turismo e dos principais países emissores de turistas.

<b>Tendências e Crescimento:</b> Identificação de tendências e crescimento do turismo ao longo dos anos.

<hr>
<br>

<h1>Tecnologias Utilizadas</h1>

<h3><b>Bibliotecas Utilizadas - Python:</b></h3>

<b>streamlit:</b> Para criar a interface gráfica do dashboard.

<b>pandas:</b> Para manipulação e análise dos dados.

<b>plotly.express:</b> Para visualização dos dados de forma interativa.

<hr>
<br>

<h1>Fonte dos Dados</h1>

Os dados foram retirados de um arquivo delimitado por vírgula, com a extensão .csv

Com as seguintes colunas

<br>

<b>country:</b> Nome do país.

<b>year:</b> Ano da observação.

<b>tourism_arrivals:</b> Número de chegadas de turistas.

<b>tourism_receipts:</b> Receita gerada pelo turismo.

<b>tourism_exports:</b> Exportações relacionadas ao turismo.

<b>tourism_departures:</b> Saídas de turistas.

<b>tourism_expenditures:</b> Gastos com turismo.

<b>gdp:</b> PIB do país.

<b>inflation:</b> Índice de inflação.

<b>unemployment:</b> Taxa de desemprego.

<hr>
<br>

<h1>Processo de ETL (Extração, Transformação e Carga)</h1>

Antes de realizar as análises, os dados passam por um tratamento que inclui:

<h3><b>Carregamento dos Dados:</b></h3>

O arquivo CSV é carregado em um DataFrame Pandas.

```python
def load_data():
    file_path = "world_tourism_economy_data.csv"
    df = pd.read_csv(file_path)
    return df

df = load_data()
```

<br>

<h3><b>Limpeza e Tratamento:</b></h3>

Remoção de valores ausentes nas colunas essenciais.

Cálculo da contribuição do turismo no PIB (tourism_contribution_gdp).

```python
df.dropna(subset=['tourism_receipts', 'tourism_arrivals', 'gdp'], inplace=True)
df['tourism_contribution_gdp'] = (df['tourism_receipts'] / df['gdp']) * 100
```

<br>

<h3><b>Criação de Novas Métricas:</b></h3>

tourism_contribution_gdp: Percentual da receita do turismo em relação ao PIB.
```python
 fig4 = px.scatter(df, x='gdp', y='tourism_receipts', color='country', title="Receita de Turismo vs PIB")
 st.plotly_chart(fig4)
```

gdp_growth: Crescimento percentual do PIB.
```python
    df['gdp_growth'] = df.groupby('country')['gdp'].pct_change()
    fig12 = px.scatter(df, x='gdp_growth', y='tourism_arrivals', color='country', title="Crescimento do PIB vs Turismo")
```

rolling_mean: Média móvel do turismo para suavizar variações anuais.
```python
df['rolling_mean'] = df.groupby('country')['tourism_arrivals'].transform(lambda x: x.rolling(3, min_periods=1).mean())
    fig11 = px.line(df, x='year', y='rolling_mean', color='country', title="Média Móvel do Turismo por País")
    st.plotly_chart(fig11)
```

<hr>
<br>

<h1>Estrutura do Dashboard</h1>

O dashboard é dividido em quatro páginas, acessíveis pelo menu lateral:
```python
st.set_page_config(page_title="Dashboard de Turismo", layout="wide")
st.sidebar.title("Navegação")
page = st.sidebar.radio("Selecione a Página", ["Turismo Global", "Turismo e Economia", "Gastos e Movimentação", "Tendências e Crescimento"])
```

<br>

<h3><b> Turismo Global</b></h3>

Foca na análise geral do turismo mundial.

<b>Gráfico 1:</b> Evolução das chegadas de turistas ao longo dos anos (linha).
```python
arrivals_by_year = df.groupby("year")['tourism_arrivals'].sum().reset_index()
    fig1 = px.line(arrivals_by_year, x='year', y='tourism_arrivals', title="Evolução das Chegadas de Turistas")
    st.plotly_chart(fig1)
```
![Gráfico 1 Pág 1](https://github.com/user-attachments/assets/4c400cda-6209-4a2c-96f7-6dbc3b9f86a5)


<br> 

<b>Gráfico 2:</b> Top 10 países com mais turistas (barras).
```python
top_countries = df.groupby("country")['tourism_arrivals'].sum().nlargest(10).reset_index()
    fig2 = px.bar(top_countries, x='country', y='tourism_arrivals', title="Top 10 Países com Mais Turistas")
    st.plotly_chart(fig2)
```
![Graf 2 pag 1](https://github.com/user-attachments/assets/b89bb700-d5ff-4600-8313-56d08e3b12bf)


<br>

<b>Gráfico 3:</b> Top 10 países com maior receita de turismo (barras).
```python
top_revenue = df.groupby("country")['tourism_receipts'].sum().nlargest(10).reset_index()
    fig3 = px.bar(top_revenue, x='country', y='tourism_receipts', title="Top 10 Países com Maior Receita de Turismo")
    st.plotly_chart(fig3)
```
![Graf 3 pag 1](https://github.com/user-attachments/assets/841061cb-ae3a-4a0b-8f02-678c8c443d06)


<hr>
<br>

<h3><b>Turismo e Economia</b></h3>

Explora a relação entre turismo e indicadores econômicos.

<b>Gráfico 1:</b> Relação entre PIB e receita do turismo (dispersão).
```python
fig4 = px.scatter(df, x='gdp', y='tourism_receipts', color='country', title="Receita de Turismo vs PIB")
    st.plotly_chart(fig4)
```
![Graf 1 pag 2](https://github.com/user-attachments/assets/e5492bc9-047a-49e7-a2c3-759a8267a568)

<br>

<b>Gráfico 2:</b> Impacto da inflação na receita do turismo (dispersão).
```python
fig5 = px.scatter(df, x='inflation', y='tourism_receipts', color='country', title="Impacto da Inflação no Turismo")
    st.plotly_chart(fig5)
```
![Graf 2 pag 2](https://github.com/user-attachments/assets/247bce33-0970-4688-b7ee-e7f16308bedd)

<br>

<b>Gráfico 3:</b> Correlação entre turismo e desemprego (dispersão).
```pyhton
fig6 = px.scatter(df, x='unemployment', y='tourism_receipts', color='country', title="Correlação entre Turismo e Desemprego")
    st.plotly_chart(fig6)
```
![Graf 3 pag 2](https://github.com/user-attachments/assets/b398d580-8969-421f-8463-a04b06c42fad)

<hr>
<br>

<h3><b>Gastos e Movimentação</h3></b>

Analisa os gastos e fluxos de turistas entre os países.

<b>Gráfico 1:</b> Relação entre exportações e gastos com turismo (dispersão).
```python
fig7 = px.scatter(df, x='tourism_exports', y='tourism_expenditures', color='country', title="Exportações vs Gastos com Turismo")
    st.plotly_chart(fig7)
```
![Graf 1 pag 3](https://github.com/user-attachments/assets/924416b5-a803-400f-9b7f-db61e608923d)

<br>

<b>Gráfico 2:</b> Top 10 países emissores de turistas (barras).
```python
top_departures = df.groupby("country")['tourism_departures'].sum().nlargest(10).reset_index()
    fig8 = px.bar(top_departures, x='country', y='tourism_departures', title="Top 10 Países que Mais Emitem Turistas")
    st.plotly_chart(fig8)
```
![Graf 2 pag 3](https://github.com/user-attachments/assets/8b3e1fc5-6709-4063-a416-654b13d2128e)

<br>

<b>Gráfico 3:</b> Comparação entre turismo receptivo e emissivo (dispersão).
```python
fig9 = px.scatter(df, x='tourism_arrivals', y='tourism_departures', color='country', title="Relação entre Turismo Receptivo e Emissivo")
    st.plotly_chart(fig9)
```
![Graf 3 pag 3](https://github.com/user-attachments/assets/5870ccd6-0317-47d0-9dc6-c2507d9367fc)

<hr>
<br>

<h3><b>Tendências e Crescimento</b></h3>

Identifica tendências e padrões de crescimento do turismo.

<b>Gráfico 1:</b> Crescimento percentual do turismo ao longo dos anos (linha).
```python
 growth = df.groupby("year")['tourism_arrivals'].sum().pct_change().reset_index()
    fig10 = px.line(growth, x='year', y='tourism_arrivals', title="Crescimento Percentual do Turismo ao Longo dos Anos")
    st.plotly_chart(fig10)
```
![Graf 1 pag 4](https://github.com/user-attachments/assets/4714ea6b-07a0-4005-b8da-7f74513ed3a8)

<br>

<b>Gráfico 2:</b> Média móvel de turismo por país (linha).
```python
df['rolling_mean'] = df.groupby('country')['tourism_arrivals'].transform(lambda x: x.rolling(3, min_periods=1).mean())
    fig11 = px.line(df, x='year', y='rolling_mean', color='country', title="Média Móvel do Turismo por País")
    st.plotly_chart(fig11)
```
![Graf 2 pag 4](https://github.com/user-attachments/assets/4dac979b-1eef-4896-a452-4d1f83cc2b95)

<br>

<b>Gráfico 3:</b> Relação entre crescimento do PIB e turismo (dispersão).
```python
df['gdp_growth'] = df.groupby('country')['gdp'].pct_change()
    fig12 = px.scatter(df, x='gdp_growth', y='tourism_arrivals', color='country', title="Crescimento do PIB vs Turismo")
    st.plotly_chart(fig12)
```
![Graf 3 pag 4](https://github.com/user-attachments/assets/46f7de08-2dd4-4f74-93a8-88ceab23efc4)

<hr>
<br>



