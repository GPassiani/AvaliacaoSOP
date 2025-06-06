# AvaliacaoSOP
Avaliação
  GNU nano 7.2                                             app.py *                                                     import streamlit as st                                                                                                  import pandas as pd                                                                                                     import matplotlib.pyplot as plt                                                                                                                                                                                                                 st.set_page_config(page_title="Análise Financeira", layout="wide")                                                                                                                                                                              st.title("📊 Análise Financeira com Streamlit")                                                                                                                                                                                                 # Carregar o dataset                                                                                                    # Carregar o CSV                                                                                                        df = pd.read_csv('ms_financial.csv', sep=';')                                                                                                                                                                                                   # Corrigir os nomes das colunas (remover espaços)                                                                       df.columns = df.columns.str.strip()                                                                                                                                                                                                             # Limpar a coluna 'Sales'                                                                                               df['Sales'] = (df['Sales']                                                                                                              .astype(str)                                                                                                            .str.replace('$', '', regex=False)                                                                                      .str.replace('.', '', regex=False)  # Remove ponto dos milhares                                                         .str.replace(',', '.', regex=False)  # Troca vírgula por ponto decimal                                                 )                                                                                                                                                                                                                                # Converter para número                                                                                                 df['Sales'] = pd.to_numeric(df['Sales'], errors='coerce')  

#Mostrar dataframe carregado
st.subheader("🗒️ Dados carregados:")
st.dataframe(df.head())                                                                                        
if 'Segment' not in df.columns:
    st.error("❌ Coluna 'Segment' não encontrada no CSV.")
    st.stop()

# Agrupar os dados
vendas_segmento = df.groupby('Segment')['Sales'].sum().reset_index()

st.subheader("📊 Total de Vendas por Segmento")
st.dataframe(vendas_segmento)

# Plotar gráfico
fig, ax = plt.subplots(figsize=(8, 5))
ax.bar(vendas_segmento['Segment'], vendas_segmento['Sales'], color='skyblue')
ax.set_xlabel('Segmento')
ax.set_ylabel('Total de Vendas')
ax.set_title('Total de Vendas por Segmento')
plt.xticks(rotation=45)

st.pyplot(fig)
ccccc  GNU nano 7.2                                             app.py                                                 ># Mostrar dataframe carregado
st.subheader("📄 Dados carregados:")
st.dataframe(df.head())

# Verificar existência da coluna 'Segment'
if 'Segment' not in df.columns:                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                
