import streamlit as st
import pandas as pd
import pandas_datareader.data as web
import numpy as np
import plotly.graph_objects as go
from plotly.subplots import make_subplots
from datetime import datetime
import yfinance as yf

yf.pdr_override()


st.sidebar.title('Menu')

#lista das empresas - ticketB3

empresas = ['PETR4.SA','AMER3.SA']
selecao = st.sidebar.selectbox('SELECIONE A EMPRESA:',empresas)

#RANGE

range = st.sidebar.slider('Período de seleção',0,12,1, key='BARRA DE SELEÇÃO')
selecao_range = str(range) + 'mo'

#colunas

col1,col2 = st.columns([0.9,0.1])
imagems =['https://files.tecnoblog.net/wp-content/uploads/2022/02/logo-americanas.png','https://upload.wikimedia.org/wikipedia/commons/5/51/Logo_petrobras.gif']


if selecao == 'AMER3.SA':
    col2.image(imagems[0],width=70)
if selecao == 'PETR4.SA':
    col2.image(imagems[1],width=70)

#titulo

titulo = f'Análise Econômica {str(selecao)}'

#coletar API YAHOO

dados = web.get_data_yahoo(selecao,period=selecao_range)


grafico_candle = go.Figure(
    data =[
        go.Candlestick(x=dados.index,
                       open=dados['Open'],
                       high=dados['High'],
                       low=dados['Low'],
                       close=dados['Close'])
    ]
)


grafico_candle.update_layout(
    xaxis_rangeslider_visible=False,
    title = 'Analise de fechamento',
    xaxis_title='Periodo',
    yaxis_title='Preço de Fechamento'
)

#enviar o grafico para o streamlit
st.plotly_chart(grafico_candle)

if st.checkbox('TABELA'):
    st.subheader('TABELA DE REGISTROS')
    st.write(dados)



