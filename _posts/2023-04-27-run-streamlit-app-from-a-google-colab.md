---
layout: post
title: Run streamlit app from a Google Colab Notebook
categories: Colab, Streamlit, Python
description: Run streamlit app from a Google Colab Notebook
keywords: Colab, streamlit, Python3
---

Run streamlit app from a Google Colab Notebook in 7 steps

## Step 1: Install streamlit framework in colab


```
!pip install -q streamlit
```

## Step 2: Create a streamlit app example

```
%%writefile app.py
import streamlit as st
import pandas as pd
import numpy as np

st.title('Gráficos com streamlit e colab')

DATE_COLUMN = 'date/time'
DATA_URL = ('https://s3-us-west-2.amazonaws.com/'
         'streamlit-demo-data/uber-raw-data-sep14.csv.gz')

def load_data(nrows):
    data = pd.read_csv(DATA_URL, nrows=nrows)
    lowercase = lambda x: str(x).lower()
    data.rename(lowercase, axis='columns', inplace=True)
    data[DATE_COLUMN] = pd.to_datetime(data[DATE_COLUMN])
    return data

data_load_state = st.text('Loading data...')
data = load_data(100)
data_load_state.text('Loading data...done!')
st.write(data)

chart_data = pd.DataFrame(
    np.random.randn(20, 3),
    columns=["a", "b", "c"])

st.bar_chart(chart_data)
```

## Step 3: verify and list files created

```
! ls -la  # list the files

! cat app.py  # visualize python file content
```

## Step 4: Install localtunnel

```
!npm install localtunnel
```

## Step 5: Run streamlit in background

```
!streamlit run app.py &>/content/logs.txt &
```

## Step 6: Expose the port 8501

```
!npx localtunnel --port 8501
```

## Step 7: Enjoy your dahsword in streamlit

a link will be generated, access the link **`https:// ....loca.lt`** 

a log.txt file will be created to save possible errors.

[<img height="40px" src="https://www.ko-fi.com/img/githubbutton_sm.svg"/>](https://ko-fi.com/latindev)