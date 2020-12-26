# Teste Processo Seletivo Maia

# Importacao da biblioteca
import os
import pandas as to_csv
import pandas as DataFrame
import pandas as pd
import requests
from bs4 import BeautifulSoup

# Requisicao da pagina
req = requests.get('https://gauchazh.clicrbs.com.br/esportes/tabelas/brasileirao')
if req.status_code == 200:
    content = req.content

# Armazenando dados da html
soup = BeautifulSoup(content, 'html.parser')
table = soup.find_all('table')
table_str = str(table)

# Armazenando dados da tabela
df = pd.read_html(table_str)[0]
df2 = pd.read_html(table_str)[1]
df2 = df2.drop(columns=['Histórico'])

# Escrevendo no excel os dados
excel = pd.ExcelWriter('desafio_Gustavo.xlsx', engine='xlsxwriter')
df.to_excel(excel, sheet_name='Tabela Brasileirao',index = False)
df2.to_excel(excel, sheet_name='Tabela Brasileirao',index = False,startcol = 1)
excel.save()
