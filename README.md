# DataBlast_TechAssessment

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import pandas_datareader as dr

start_date = '2021-01-01'
end_date = '2021-01-10'

usdjpy = dr.data.DataReader('USDJPY%3DX', data_source='yahoo', start=start_date, end=end_date)
usdpgk = dr.data.DataReader('USDPGK%3DX', data_source='yahoo', start=start_date, end=end_date)
usdxpf = dr.data.DataReader('USDXPF%3DX', data_source='yahoo', start=start_date, end=end_date)
usdmga = dr.data.DataReader('USDMGA%3DX', data_source='yahoo', start=start_date, end=end_date)
usdeur = dr.data.DataReader('EURUSD%3DX', data_source='yahoo', start=start_date, end=end_date)

usdjpy.drop(["High","Low","Open","Volume","Adj Close"], axis=1,inplace=True)
usdpgk.drop(["High","Low","Open","Volume","Adj Close"], axis=1,inplace=True)
usdxpf.drop(["High","Low","Open","Volume","Adj Close"], axis=1,inplace=True)
usdmga.drop(["High","Low","Open","Volume","Adj Close"], axis=1,inplace=True)
usdeur.drop(["High","Low","Open","Volume","Adj Close"], axis=1,inplace=True)


usdjpy["name"]="JPY"
usdpgk["name"]="PGK"
usdxpf["name"]="XPF"
usdmga["name"]="MGA"
usdeur["name"]="EUR"

usdjpy = usdjpy[["name"] + usdjpy.columns[:-1].tolist()]
usdpgk = usdpgk[["name"] + usdpgk.columns[:-1].tolist()]
usdxpf = usdxpf[["name"] + usdxpf.columns[:-1].tolist()]
usdmga = usdmga[["name"] + usdmga.columns[:-1].tolist()]
usdeur = usdeur[["name"] + usdeur.columns[:-1].tolist()]


usdjpy.rename(columns ={'Close':'value'},inplace=True)
usdpgk.rename(columns ={'Close':'value'},inplace=True)
usdxpf.rename(columns ={'Close':'value'},inplace=True)
usdmga.rename(columns ={'Close':'value'},inplace=True)
usdeur.rename(columns ={'Close':'value'},inplace=True)

Currency=pd.concat([usdjpy,usdpgk,usdxpf,usdmga,usdeur],axis=0)
Currency.sort_values("name")
print(Currency)


Currency.to_csv('Currency.csv', index=False)
