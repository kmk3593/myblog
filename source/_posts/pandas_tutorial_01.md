---
title: "pandas_tutorial_01"
tags:
  - python
categories:
  - python
  - pandas
  - tutorial
author: "minkuen"
date: '2022-03-23'
---

### 데이터 전처리
- 데이터 전처리의 기본
  - garbage Data ---[ Great Model ]---> Garbage Results

데이터 전처리의 주요 과정
- 데이터 전처리 수행 프로세스***(중요)***
  - 1.중복값 제거 및 결측치 처리  ->  2.이상치 처리  ->  3.Feature Engineering
  - 주요 목적 : 더 나은 분석 결과 도출 및 모형 성능 개선 실현




pandas 기본자료형
- 숫자, 문자 모두 들어간다.
- 중복이 불가능하다.


# 판다스

### 라이브러리 불러오기


```python
import pandas as pd
print(pd.__version__)
```

    1.3.5
    

### 테스트


```python
temp_dic = {"col1": [1,2,3],
            "col2": [3, 4, 5]}

df = pd.DataFrame(temp_dic) # DataFrame() 사용
df
```





  <div id="df-5f12a67d-363f-495e-a8d6-e15402e0c5d6">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>col1</th>
      <th>col2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-5f12a67d-363f-495e-a8d6-e15402e0c5d6')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-5f12a67d-363f-495e-a8d6-e15402e0c5d6 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-5f12a67d-363f-495e-a8d6-e15402e0c5d6');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
print(type(df))
```

    <class 'pandas.core.frame.DataFrame'>
    


```python
temp_dic = {'a':1, 'b':2, 'c':3}
ser = pd.Series(temp_dic) # Series() 사용
print(ser)
print(type(ser))
```

    a    1
    b    2
    c    3
    dtype: int64
    <class 'pandas.core.series.Series'>
    

### 구글 드라이브 연동
- 구글 드라이브 → colab notebook → 새 폴더 생성 : data → 슬랙에서 다운 받은 lemonade.csv 파일을 올린다 -> 다음 코드를 실행


```python
from google.colab import drive
drive.mount('/content/drive')
```

    Mounted at /content/drive
    

Mounted at ..drive 가 출력되었으므로 성공

현재 좌측에 폴더 그림 -> drive -> mydrive -> Colab Notebooks -> data -> Lemonade2016.csv를 찾아서 우클릭 -> 경로 복사 -> 다음 코드에 붙여넣어 사용


```python
DATA_PATH = '/content/drive/MyDrive/Colab Notebooks/data/Lemonade2016.csv'
juice = pd.read_csv(DATA_PATH)
juice
```





  <div id="df-e4ed5b94-20e7-42ba-9f65-459f54e1728a">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Location</th>
      <th>Lemon</th>
      <th>Orange</th>
      <th>Temperature</th>
      <th>Leaflets</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>7/1/2016</td>
      <td>Park</td>
      <td>97</td>
      <td>67</td>
      <td>70</td>
      <td>90.0</td>
      <td>0.25</td>
    </tr>
    <tr>
      <th>1</th>
      <td>7/2/2016</td>
      <td>Park</td>
      <td>98</td>
      <td>67</td>
      <td>72</td>
      <td>90.0</td>
      <td>0.25</td>
    </tr>
    <tr>
      <th>2</th>
      <td>7/3/2016</td>
      <td>Park</td>
      <td>110</td>
      <td>77</td>
      <td>71</td>
      <td>104.0</td>
      <td>0.25</td>
    </tr>
    <tr>
      <th>3</th>
      <td>7/4/2016</td>
      <td>Beach</td>
      <td>134</td>
      <td>99</td>
      <td>76</td>
      <td>98.0</td>
      <td>0.25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>7/5/2016</td>
      <td>Beach</td>
      <td>159</td>
      <td>118</td>
      <td>78</td>
      <td>135.0</td>
      <td>0.25</td>
    </tr>
    <tr>
      <th>5</th>
      <td>7/6/2016</td>
      <td>Beach</td>
      <td>103</td>
      <td>69</td>
      <td>82</td>
      <td>90.0</td>
      <td>0.25</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7/6/2016</td>
      <td>Beach</td>
      <td>103</td>
      <td>69</td>
      <td>82</td>
      <td>90.0</td>
      <td>0.25</td>
    </tr>
    <tr>
      <th>7</th>
      <td>7/7/2016</td>
      <td>Beach</td>
      <td>143</td>
      <td>101</td>
      <td>81</td>
      <td>135.0</td>
      <td>0.25</td>
    </tr>
    <tr>
      <th>8</th>
      <td>NaN</td>
      <td>Beach</td>
      <td>123</td>
      <td>86</td>
      <td>82</td>
      <td>113.0</td>
      <td>0.25</td>
    </tr>
    <tr>
      <th>9</th>
      <td>7/9/2016</td>
      <td>Beach</td>
      <td>134</td>
      <td>95</td>
      <td>80</td>
      <td>126.0</td>
      <td>0.25</td>
    </tr>
    <tr>
      <th>10</th>
      <td>7/10/2016</td>
      <td>Beach</td>
      <td>140</td>
      <td>98</td>
      <td>82</td>
      <td>131.0</td>
      <td>0.25</td>
    </tr>
    <tr>
      <th>11</th>
      <td>7/11/2016</td>
      <td>Beach</td>
      <td>162</td>
      <td>120</td>
      <td>83</td>
      <td>135.0</td>
      <td>0.25</td>
    </tr>
    <tr>
      <th>12</th>
      <td>7/12/2016</td>
      <td>Beach</td>
      <td>130</td>
      <td>95</td>
      <td>84</td>
      <td>99.0</td>
      <td>0.25</td>
    </tr>
    <tr>
      <th>13</th>
      <td>7/13/2016</td>
      <td>Beach</td>
      <td>109</td>
      <td>75</td>
      <td>77</td>
      <td>99.0</td>
      <td>0.25</td>
    </tr>
    <tr>
      <th>14</th>
      <td>7/14/2016</td>
      <td>Beach</td>
      <td>122</td>
      <td>85</td>
      <td>78</td>
      <td>113.0</td>
      <td>0.25</td>
    </tr>
    <tr>
      <th>15</th>
      <td>7/15/2016</td>
      <td>Beach</td>
      <td>98</td>
      <td>62</td>
      <td>75</td>
      <td>108.0</td>
      <td>0.50</td>
    </tr>
    <tr>
      <th>16</th>
      <td>7/16/2016</td>
      <td>Beach</td>
      <td>81</td>
      <td>50</td>
      <td>74</td>
      <td>90.0</td>
      <td>0.50</td>
    </tr>
    <tr>
      <th>17</th>
      <td>7/17/2016</td>
      <td>Beach</td>
      <td>115</td>
      <td>76</td>
      <td>77</td>
      <td>126.0</td>
      <td>0.50</td>
    </tr>
    <tr>
      <th>18</th>
      <td>7/18/2016</td>
      <td>Park</td>
      <td>131</td>
      <td>92</td>
      <td>81</td>
      <td>122.0</td>
      <td>0.50</td>
    </tr>
    <tr>
      <th>19</th>
      <td>7/19/2016</td>
      <td>Park</td>
      <td>122</td>
      <td>85</td>
      <td>78</td>
      <td>113.0</td>
      <td>0.50</td>
    </tr>
    <tr>
      <th>20</th>
      <td>7/20/2016</td>
      <td>Park</td>
      <td>71</td>
      <td>42</td>
      <td>70</td>
      <td>NaN</td>
      <td>0.50</td>
    </tr>
    <tr>
      <th>21</th>
      <td>7/21/2016</td>
      <td>Park</td>
      <td>83</td>
      <td>50</td>
      <td>77</td>
      <td>90.0</td>
      <td>0.50</td>
    </tr>
    <tr>
      <th>22</th>
      <td>7/22/2016</td>
      <td>Park</td>
      <td>112</td>
      <td>75</td>
      <td>80</td>
      <td>108.0</td>
      <td>0.50</td>
    </tr>
    <tr>
      <th>23</th>
      <td>7/23/2016</td>
      <td>Park</td>
      <td>120</td>
      <td>82</td>
      <td>81</td>
      <td>117.0</td>
      <td>0.50</td>
    </tr>
    <tr>
      <th>24</th>
      <td>7/24/2016</td>
      <td>Park</td>
      <td>121</td>
      <td>82</td>
      <td>82</td>
      <td>117.0</td>
      <td>0.50</td>
    </tr>
    <tr>
      <th>25</th>
      <td>7/25/2016</td>
      <td>Park</td>
      <td>156</td>
      <td>113</td>
      <td>84</td>
      <td>135.0</td>
      <td>0.50</td>
    </tr>
    <tr>
      <th>26</th>
      <td>7/26/2016</td>
      <td>Park</td>
      <td>176</td>
      <td>129</td>
      <td>83</td>
      <td>158.0</td>
      <td>0.35</td>
    </tr>
    <tr>
      <th>27</th>
      <td>7/27/2016</td>
      <td>Park</td>
      <td>104</td>
      <td>68</td>
      <td>80</td>
      <td>99.0</td>
      <td>0.35</td>
    </tr>
    <tr>
      <th>28</th>
      <td>7/28/2016</td>
      <td>Park</td>
      <td>96</td>
      <td>63</td>
      <td>82</td>
      <td>90.0</td>
      <td>0.35</td>
    </tr>
    <tr>
      <th>29</th>
      <td>7/29/2016</td>
      <td>Park</td>
      <td>100</td>
      <td>66</td>
      <td>81</td>
      <td>95.0</td>
      <td>0.35</td>
    </tr>
    <tr>
      <th>30</th>
      <td>7/30/2016</td>
      <td>Beach</td>
      <td>88</td>
      <td>57</td>
      <td>82</td>
      <td>81.0</td>
      <td>0.35</td>
    </tr>
    <tr>
      <th>31</th>
      <td>7/31/2016</td>
      <td>Beach</td>
      <td>76</td>
      <td>47</td>
      <td>82</td>
      <td>68.0</td>
      <td>0.35</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-e4ed5b94-20e7-42ba-9f65-459f54e1728a')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-e4ed5b94-20e7-42ba-9f65-459f54e1728a button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-e4ed5b94-20e7-42ba-9f65-459f54e1728a');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




- 데이터를 불러왔다.
- 첫번째 파악해야 하는 것!  
  - 데이터 구조를 파악해보자


```python
juice.info()  # 데이터 구조 파악
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 32 entries, 0 to 31
    Data columns (total 7 columns):
     #   Column       Non-Null Count  Dtype  
    ---  ------       --------------  -----  
     0   Date         31 non-null     object 
     1   Location     32 non-null     object 
     2   Lemon        32 non-null     int64  
     3   Orange       32 non-null     int64  
     4   Temperature  32 non-null     int64  
     5   Leaflets     31 non-null     float64
     6   Price        32 non-null     float64
    dtypes: float64(2), int64(3), object(2)
    memory usage: 1.9+ KB
    


```python
juice.head()  # 상위의 데이터를 여러개 불러온다. 디폴트 값이 5개.
```





  <div id="df-c3238942-1033-4010-80b8-10e94c66dc23">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Location</th>
      <th>Lemon</th>
      <th>Orange</th>
      <th>Temperature</th>
      <th>Leaflets</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>7/1/2016</td>
      <td>Park</td>
      <td>97</td>
      <td>67</td>
      <td>70</td>
      <td>90.0</td>
      <td>0.25</td>
    </tr>
    <tr>
      <th>1</th>
      <td>7/2/2016</td>
      <td>Park</td>
      <td>98</td>
      <td>67</td>
      <td>72</td>
      <td>90.0</td>
      <td>0.25</td>
    </tr>
    <tr>
      <th>2</th>
      <td>7/3/2016</td>
      <td>Park</td>
      <td>110</td>
      <td>77</td>
      <td>71</td>
      <td>104.0</td>
      <td>0.25</td>
    </tr>
    <tr>
      <th>3</th>
      <td>7/4/2016</td>
      <td>Beach</td>
      <td>134</td>
      <td>99</td>
      <td>76</td>
      <td>98.0</td>
      <td>0.25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>7/5/2016</td>
      <td>Beach</td>
      <td>159</td>
      <td>118</td>
      <td>78</td>
      <td>135.0</td>
      <td>0.25</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-c3238942-1033-4010-80b8-10e94c66dc23')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-c3238942-1033-4010-80b8-10e94c66dc23 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-c3238942-1033-4010-80b8-10e94c66dc23');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
juice.tail()  # 하위의 데이터를 여러개 불러온다. 디폴트 값이 5개
```





  <div id="df-cc60af2a-dd96-48c1-9398-546b4a947c77">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Location</th>
      <th>Lemon</th>
      <th>Orange</th>
      <th>Temperature</th>
      <th>Leaflets</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>27</th>
      <td>7/27/2016</td>
      <td>Park</td>
      <td>104</td>
      <td>68</td>
      <td>80</td>
      <td>99.0</td>
      <td>0.35</td>
    </tr>
    <tr>
      <th>28</th>
      <td>7/28/2016</td>
      <td>Park</td>
      <td>96</td>
      <td>63</td>
      <td>82</td>
      <td>90.0</td>
      <td>0.35</td>
    </tr>
    <tr>
      <th>29</th>
      <td>7/29/2016</td>
      <td>Park</td>
      <td>100</td>
      <td>66</td>
      <td>81</td>
      <td>95.0</td>
      <td>0.35</td>
    </tr>
    <tr>
      <th>30</th>
      <td>7/30/2016</td>
      <td>Beach</td>
      <td>88</td>
      <td>57</td>
      <td>82</td>
      <td>81.0</td>
      <td>0.35</td>
    </tr>
    <tr>
      <th>31</th>
      <td>7/31/2016</td>
      <td>Beach</td>
      <td>76</td>
      <td>47</td>
      <td>82</td>
      <td>68.0</td>
      <td>0.35</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-cc60af2a-dd96-48c1-9398-546b4a947c77')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-cc60af2a-dd96-48c1-9398-546b4a947c77 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-cc60af2a-dd96-48c1-9398-546b4a947c77');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




- Describe() 함수
  -  기술통계량 확인해주는 함수


```python
juice.describe()
```





  <div id="df-bfd69db7-f9d2-49ea-84ed-2989ca9e02a8">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Lemon</th>
      <th>Orange</th>
      <th>Temperature</th>
      <th>Leaflets</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>32.000000</td>
      <td>32.000000</td>
      <td>32.000000</td>
      <td>31.000000</td>
      <td>32.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>116.156250</td>
      <td>80.000000</td>
      <td>78.968750</td>
      <td>108.548387</td>
      <td>0.354687</td>
    </tr>
    <tr>
      <th>std</th>
      <td>25.823357</td>
      <td>21.863211</td>
      <td>4.067847</td>
      <td>20.117718</td>
      <td>0.113137</td>
    </tr>
    <tr>
      <th>min</th>
      <td>71.000000</td>
      <td>42.000000</td>
      <td>70.000000</td>
      <td>68.000000</td>
      <td>0.250000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>98.000000</td>
      <td>66.750000</td>
      <td>77.000000</td>
      <td>90.000000</td>
      <td>0.250000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>113.500000</td>
      <td>76.500000</td>
      <td>80.500000</td>
      <td>108.000000</td>
      <td>0.350000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>131.750000</td>
      <td>95.000000</td>
      <td>82.000000</td>
      <td>124.000000</td>
      <td>0.500000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>176.000000</td>
      <td>129.000000</td>
      <td>84.000000</td>
      <td>158.000000</td>
      <td>0.500000</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-bfd69db7-f9d2-49ea-84ed-2989ca9e02a8')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-bfd69db7-f9d2-49ea-84ed-2989ca9e02a8 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-bfd69db7-f9d2-49ea-84ed-2989ca9e02a8');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
type(juice.describe())  # Describe함수 결과물의 타입은 DataFrame 이다.
```




    pandas.core.frame.DataFrame



- value_counts()


```python
print(juice['Location'].value_counts())
print(type(juice['Location'].value_counts()))
```

    Beach    17
    Park     15
    Name: Location, dtype: int64
    <class 'pandas.core.series.Series'>
    

# 데이터 다뤄보기
- 행과 열을 핸들링 해보자.


```python
juice['Sold'] = 0   # sold 열 추가.
print(juice.head(3))
```

           Date Location  Lemon  Orange  Temperature  Leaflets  Price  Sold
    0  7/1/2016     Park     97      67           70      90.0   0.25     0
    1  7/2/2016     Park     98      67           72      90.0   0.25     0
    2  7/3/2016     Park    110      77           71     104.0   0.25     0
    


```python
juice['Sold'] = juice['Lemon'] + juice['Orange']  # Sold에 값 설정
print(juice.head(3))
```

           Date Location  Lemon  Orange  Temperature  Leaflets  Price  Sold
    0  7/1/2016     Park     97      67           70      90.0   0.25   164
    1  7/2/2016     Park     98      67           72      90.0   0.25   165
    2  7/3/2016     Park    110      77           71     104.0   0.25   187
    

- 매출액 = 가격 x 판매량
- Revenue 로 만들어보자


```python
juice['Revenue'] = juice['Sold'] * juice['Price']
print(juice.head(3))
```

           Date Location  Lemon  Orange  Temperature  Leaflets  Price  Sold  \
    0  7/1/2016     Park     97      67           70      90.0   0.25   164   
    1  7/2/2016     Park     98      67           72      90.0   0.25   165   
    2  7/3/2016     Park    110      77           71     104.0   0.25   187   
    
       Revenue  
    0    41.00  
    1    41.25  
    2    46.75  
    

- drop(axis = 0|1)
  + axis는 '축'을 의미한다. 한 축을 따라서 연산이 된다.
  + axis를 0으로 설정 시, 행(=index)방향으로 drop() 실행
  + axis를 1로 설정 시, 열방향으로 drop 수행함.


```python
juice_column_drop = juice.drop('Sold', axis = 1)
print(juice_column_drop.head(3))
```

           Date Location  Lemon  Orange  Temperature  Leaflets  Price  Revenue
    0  7/1/2016     Park     97      67           70      90.0   0.25    41.00
    1  7/2/2016     Park     98      67           72      90.0   0.25    41.25
    2  7/3/2016     Park    110      77           71     104.0   0.25    46.75
    


```python
juice_row_drop = juice.drop(0, axis = 0)
print(juice_row_drop.head(3))
```

           Date Location  Lemon  Orange  Temperature  Leaflets  Price  Sold  \
    1  7/2/2016     Park     98      67           72      90.0   0.25   165   
    2  7/3/2016     Park    110      77           71     104.0   0.25   187   
    3  7/4/2016    Beach    134      99           76      98.0   0.25   233   
    
       Revenue  
    1    41.25  
    2    46.75  
    3    58.25  
    

### 데이터 인덱싱


```python
juice[0:5] 
```





  <div id="df-bfa3fabe-e933-4527-879f-12c188c0b8bd">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Location</th>
      <th>Lemon</th>
      <th>Orange</th>
      <th>Temperature</th>
      <th>Leaflets</th>
      <th>Price</th>
      <th>Sold</th>
      <th>Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>7/1/2016</td>
      <td>Park</td>
      <td>97</td>
      <td>67</td>
      <td>70</td>
      <td>90.0</td>
      <td>0.25</td>
      <td>164</td>
      <td>41.00</td>
    </tr>
    <tr>
      <th>1</th>
      <td>7/2/2016</td>
      <td>Park</td>
      <td>98</td>
      <td>67</td>
      <td>72</td>
      <td>90.0</td>
      <td>0.25</td>
      <td>165</td>
      <td>41.25</td>
    </tr>
    <tr>
      <th>2</th>
      <td>7/3/2016</td>
      <td>Park</td>
      <td>110</td>
      <td>77</td>
      <td>71</td>
      <td>104.0</td>
      <td>0.25</td>
      <td>187</td>
      <td>46.75</td>
    </tr>
    <tr>
      <th>3</th>
      <td>7/4/2016</td>
      <td>Beach</td>
      <td>134</td>
      <td>99</td>
      <td>76</td>
      <td>98.0</td>
      <td>0.25</td>
      <td>233</td>
      <td>58.25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>7/5/2016</td>
      <td>Beach</td>
      <td>159</td>
      <td>118</td>
      <td>78</td>
      <td>135.0</td>
      <td>0.25</td>
      <td>277</td>
      <td>69.25</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-bfa3fabe-e933-4527-879f-12c188c0b8bd')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-bfa3fabe-e933-4527-879f-12c188c0b8bd button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-bfa3fabe-e933-4527-879f-12c188c0b8bd');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




### boolean 값을 활용한 데이터 추출


```python
# location이 Beach인 경우
# juice['Location'].value_counts()
juice[juice['Location'] == "Beach"]
```





  <div id="df-f23f5092-ba57-4126-bdd5-ecc3581c90cd">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Location</th>
      <th>Lemon</th>
      <th>Orange</th>
      <th>Temperature</th>
      <th>Leaflets</th>
      <th>Price</th>
      <th>Sold</th>
      <th>Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>7/4/2016</td>
      <td>Beach</td>
      <td>134</td>
      <td>99</td>
      <td>76</td>
      <td>98.0</td>
      <td>0.25</td>
      <td>233</td>
      <td>58.25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>7/5/2016</td>
      <td>Beach</td>
      <td>159</td>
      <td>118</td>
      <td>78</td>
      <td>135.0</td>
      <td>0.25</td>
      <td>277</td>
      <td>69.25</td>
    </tr>
    <tr>
      <th>5</th>
      <td>7/6/2016</td>
      <td>Beach</td>
      <td>103</td>
      <td>69</td>
      <td>82</td>
      <td>90.0</td>
      <td>0.25</td>
      <td>172</td>
      <td>43.00</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7/6/2016</td>
      <td>Beach</td>
      <td>103</td>
      <td>69</td>
      <td>82</td>
      <td>90.0</td>
      <td>0.25</td>
      <td>172</td>
      <td>43.00</td>
    </tr>
    <tr>
      <th>7</th>
      <td>7/7/2016</td>
      <td>Beach</td>
      <td>143</td>
      <td>101</td>
      <td>81</td>
      <td>135.0</td>
      <td>0.25</td>
      <td>244</td>
      <td>61.00</td>
    </tr>
    <tr>
      <th>8</th>
      <td>NaN</td>
      <td>Beach</td>
      <td>123</td>
      <td>86</td>
      <td>82</td>
      <td>113.0</td>
      <td>0.25</td>
      <td>209</td>
      <td>52.25</td>
    </tr>
    <tr>
      <th>9</th>
      <td>7/9/2016</td>
      <td>Beach</td>
      <td>134</td>
      <td>95</td>
      <td>80</td>
      <td>126.0</td>
      <td>0.25</td>
      <td>229</td>
      <td>57.25</td>
    </tr>
    <tr>
      <th>10</th>
      <td>7/10/2016</td>
      <td>Beach</td>
      <td>140</td>
      <td>98</td>
      <td>82</td>
      <td>131.0</td>
      <td>0.25</td>
      <td>238</td>
      <td>59.50</td>
    </tr>
    <tr>
      <th>11</th>
      <td>7/11/2016</td>
      <td>Beach</td>
      <td>162</td>
      <td>120</td>
      <td>83</td>
      <td>135.0</td>
      <td>0.25</td>
      <td>282</td>
      <td>70.50</td>
    </tr>
    <tr>
      <th>12</th>
      <td>7/12/2016</td>
      <td>Beach</td>
      <td>130</td>
      <td>95</td>
      <td>84</td>
      <td>99.0</td>
      <td>0.25</td>
      <td>225</td>
      <td>56.25</td>
    </tr>
    <tr>
      <th>13</th>
      <td>7/13/2016</td>
      <td>Beach</td>
      <td>109</td>
      <td>75</td>
      <td>77</td>
      <td>99.0</td>
      <td>0.25</td>
      <td>184</td>
      <td>46.00</td>
    </tr>
    <tr>
      <th>14</th>
      <td>7/14/2016</td>
      <td>Beach</td>
      <td>122</td>
      <td>85</td>
      <td>78</td>
      <td>113.0</td>
      <td>0.25</td>
      <td>207</td>
      <td>51.75</td>
    </tr>
    <tr>
      <th>15</th>
      <td>7/15/2016</td>
      <td>Beach</td>
      <td>98</td>
      <td>62</td>
      <td>75</td>
      <td>108.0</td>
      <td>0.50</td>
      <td>160</td>
      <td>80.00</td>
    </tr>
    <tr>
      <th>16</th>
      <td>7/16/2016</td>
      <td>Beach</td>
      <td>81</td>
      <td>50</td>
      <td>74</td>
      <td>90.0</td>
      <td>0.50</td>
      <td>131</td>
      <td>65.50</td>
    </tr>
    <tr>
      <th>17</th>
      <td>7/17/2016</td>
      <td>Beach</td>
      <td>115</td>
      <td>76</td>
      <td>77</td>
      <td>126.0</td>
      <td>0.50</td>
      <td>191</td>
      <td>95.50</td>
    </tr>
    <tr>
      <th>30</th>
      <td>7/30/2016</td>
      <td>Beach</td>
      <td>88</td>
      <td>57</td>
      <td>82</td>
      <td>81.0</td>
      <td>0.35</td>
      <td>145</td>
      <td>50.75</td>
    </tr>
    <tr>
      <th>31</th>
      <td>7/31/2016</td>
      <td>Beach</td>
      <td>76</td>
      <td>47</td>
      <td>82</td>
      <td>68.0</td>
      <td>0.35</td>
      <td>123</td>
      <td>43.05</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-f23f5092-ba57-4126-bdd5-ecc3581c90cd')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-f23f5092-ba57-4126-bdd5-ecc3581c90cd button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-f23f5092-ba57-4126-bdd5-ecc3581c90cd');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
# location이 Beach인 경우
# juice['Location'].value_counts()
juice[juice['Leaflets'] >= 100]
```





  <div id="df-080b31c4-9d87-4d46-a98d-5d6eec44b68f">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Location</th>
      <th>Lemon</th>
      <th>Orange</th>
      <th>Temperature</th>
      <th>Leaflets</th>
      <th>Price</th>
      <th>Sold</th>
      <th>Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>7/3/2016</td>
      <td>Park</td>
      <td>110</td>
      <td>77</td>
      <td>71</td>
      <td>104.0</td>
      <td>0.25</td>
      <td>187</td>
      <td>46.75</td>
    </tr>
    <tr>
      <th>4</th>
      <td>7/5/2016</td>
      <td>Beach</td>
      <td>159</td>
      <td>118</td>
      <td>78</td>
      <td>135.0</td>
      <td>0.25</td>
      <td>277</td>
      <td>69.25</td>
    </tr>
    <tr>
      <th>7</th>
      <td>7/7/2016</td>
      <td>Beach</td>
      <td>143</td>
      <td>101</td>
      <td>81</td>
      <td>135.0</td>
      <td>0.25</td>
      <td>244</td>
      <td>61.00</td>
    </tr>
    <tr>
      <th>8</th>
      <td>NaN</td>
      <td>Beach</td>
      <td>123</td>
      <td>86</td>
      <td>82</td>
      <td>113.0</td>
      <td>0.25</td>
      <td>209</td>
      <td>52.25</td>
    </tr>
    <tr>
      <th>9</th>
      <td>7/9/2016</td>
      <td>Beach</td>
      <td>134</td>
      <td>95</td>
      <td>80</td>
      <td>126.0</td>
      <td>0.25</td>
      <td>229</td>
      <td>57.25</td>
    </tr>
    <tr>
      <th>10</th>
      <td>7/10/2016</td>
      <td>Beach</td>
      <td>140</td>
      <td>98</td>
      <td>82</td>
      <td>131.0</td>
      <td>0.25</td>
      <td>238</td>
      <td>59.50</td>
    </tr>
    <tr>
      <th>11</th>
      <td>7/11/2016</td>
      <td>Beach</td>
      <td>162</td>
      <td>120</td>
      <td>83</td>
      <td>135.0</td>
      <td>0.25</td>
      <td>282</td>
      <td>70.50</td>
    </tr>
    <tr>
      <th>14</th>
      <td>7/14/2016</td>
      <td>Beach</td>
      <td>122</td>
      <td>85</td>
      <td>78</td>
      <td>113.0</td>
      <td>0.25</td>
      <td>207</td>
      <td>51.75</td>
    </tr>
    <tr>
      <th>15</th>
      <td>7/15/2016</td>
      <td>Beach</td>
      <td>98</td>
      <td>62</td>
      <td>75</td>
      <td>108.0</td>
      <td>0.50</td>
      <td>160</td>
      <td>80.00</td>
    </tr>
    <tr>
      <th>17</th>
      <td>7/17/2016</td>
      <td>Beach</td>
      <td>115</td>
      <td>76</td>
      <td>77</td>
      <td>126.0</td>
      <td>0.50</td>
      <td>191</td>
      <td>95.50</td>
    </tr>
    <tr>
      <th>18</th>
      <td>7/18/2016</td>
      <td>Park</td>
      <td>131</td>
      <td>92</td>
      <td>81</td>
      <td>122.0</td>
      <td>0.50</td>
      <td>223</td>
      <td>111.50</td>
    </tr>
    <tr>
      <th>19</th>
      <td>7/19/2016</td>
      <td>Park</td>
      <td>122</td>
      <td>85</td>
      <td>78</td>
      <td>113.0</td>
      <td>0.50</td>
      <td>207</td>
      <td>103.50</td>
    </tr>
    <tr>
      <th>22</th>
      <td>7/22/2016</td>
      <td>Park</td>
      <td>112</td>
      <td>75</td>
      <td>80</td>
      <td>108.0</td>
      <td>0.50</td>
      <td>187</td>
      <td>93.50</td>
    </tr>
    <tr>
      <th>23</th>
      <td>7/23/2016</td>
      <td>Park</td>
      <td>120</td>
      <td>82</td>
      <td>81</td>
      <td>117.0</td>
      <td>0.50</td>
      <td>202</td>
      <td>101.00</td>
    </tr>
    <tr>
      <th>24</th>
      <td>7/24/2016</td>
      <td>Park</td>
      <td>121</td>
      <td>82</td>
      <td>82</td>
      <td>117.0</td>
      <td>0.50</td>
      <td>203</td>
      <td>101.50</td>
    </tr>
    <tr>
      <th>25</th>
      <td>7/25/2016</td>
      <td>Park</td>
      <td>156</td>
      <td>113</td>
      <td>84</td>
      <td>135.0</td>
      <td>0.50</td>
      <td>269</td>
      <td>134.50</td>
    </tr>
    <tr>
      <th>26</th>
      <td>7/26/2016</td>
      <td>Park</td>
      <td>176</td>
      <td>129</td>
      <td>83</td>
      <td>158.0</td>
      <td>0.35</td>
      <td>305</td>
      <td>106.75</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-080b31c4-9d87-4d46-a98d-5d6eec44b68f')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-080b31c4-9d87-4d46-a98d-5d6eec44b68f button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-080b31c4-9d87-4d46-a98d-5d6eec44b68f');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




### iloc vs loc
- 차이를 확인한다!


```python
juice.head(3)
# index 번호는 다음 실행 결과에서
#     0      1        2       3         4            5          6       7      8
```





  <div id="df-dadb1a11-c681-42a1-9b8b-85510d760ea0">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Location</th>
      <th>Lemon</th>
      <th>Orange</th>
      <th>Temperature</th>
      <th>Leaflets</th>
      <th>Price</th>
      <th>Sold</th>
      <th>Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>7/1/2016</td>
      <td>Park</td>
      <td>97</td>
      <td>67</td>
      <td>70</td>
      <td>90.0</td>
      <td>0.25</td>
      <td>164</td>
      <td>41.00</td>
    </tr>
    <tr>
      <th>1</th>
      <td>7/2/2016</td>
      <td>Park</td>
      <td>98</td>
      <td>67</td>
      <td>72</td>
      <td>90.0</td>
      <td>0.25</td>
      <td>165</td>
      <td>41.25</td>
    </tr>
    <tr>
      <th>2</th>
      <td>7/3/2016</td>
      <td>Park</td>
      <td>110</td>
      <td>77</td>
      <td>71</td>
      <td>104.0</td>
      <td>0.25</td>
      <td>187</td>
      <td>46.75</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-dadb1a11-c681-42a1-9b8b-85510d760ea0')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-dadb1a11-c681-42a1-9b8b-85510d760ea0 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-dadb1a11-c681-42a1-9b8b-85510d760ea0');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




%%time 
- 실행 시간 측정
- 코드의 효율을 살펴보자


```python
%%time

juice.iloc[0:3, 0:2]  # 인덱스 기반
```

    CPU times: user 2.14 ms, sys: 0 ns, total: 2.14 ms
    Wall time: 3.19 ms
    





  <div id="df-dfd7fd78-f2b8-491f-a422-bd0e37bc0297">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Location</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>7/1/2016</td>
      <td>Park</td>
    </tr>
    <tr>
      <th>1</th>
      <td>7/2/2016</td>
      <td>Park</td>
    </tr>
    <tr>
      <th>2</th>
      <td>7/3/2016</td>
      <td>Park</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-dfd7fd78-f2b8-491f-a422-bd0e37bc0297')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-dfd7fd78-f2b8-491f-a422-bd0e37bc0297 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-dfd7fd78-f2b8-491f-a422-bd0e37bc0297');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




- loc
- -> 라벨 기반


```python
%%time

juice.loc[0:2, ['Date', 'Location']]  # 라벨 기반이라 0:2로 실행 시, 3개 생성된다
```

    CPU times: user 1.64 ms, sys: 0 ns, total: 1.64 ms
    Wall time: 1.62 ms
    





  <div id="df-f63e27df-425e-4e52-acd7-6c213c3c886a">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Location</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>7/1/2016</td>
      <td>Park</td>
    </tr>
    <tr>
      <th>1</th>
      <td>7/2/2016</td>
      <td>Park</td>
    </tr>
    <tr>
      <th>2</th>
      <td>7/3/2016</td>
      <td>Park</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-f63e27df-425e-4e52-acd7-6c213c3c886a')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-f63e27df-425e-4e52-acd7-6c213c3c886a button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-f63e27df-425e-4e52-acd7-6c213c3c886a');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
# juice[juice['Leaflets'] >= 100, 컬럼명 별도 추출]

juice.loc[juice['Leaflets'] >= 100, ['Date', 'Location']] # 컬럼은 컬럼별로 추출
```





  <div id="df-80c7ea4c-f3b6-416c-90a6-935ca4d10c87">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Location</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>7/3/2016</td>
      <td>Park</td>
    </tr>
    <tr>
      <th>4</th>
      <td>7/5/2016</td>
      <td>Beach</td>
    </tr>
    <tr>
      <th>7</th>
      <td>7/7/2016</td>
      <td>Beach</td>
    </tr>
    <tr>
      <th>8</th>
      <td>NaN</td>
      <td>Beach</td>
    </tr>
    <tr>
      <th>9</th>
      <td>7/9/2016</td>
      <td>Beach</td>
    </tr>
    <tr>
      <th>10</th>
      <td>7/10/2016</td>
      <td>Beach</td>
    </tr>
    <tr>
      <th>11</th>
      <td>7/11/2016</td>
      <td>Beach</td>
    </tr>
    <tr>
      <th>14</th>
      <td>7/14/2016</td>
      <td>Beach</td>
    </tr>
    <tr>
      <th>15</th>
      <td>7/15/2016</td>
      <td>Beach</td>
    </tr>
    <tr>
      <th>17</th>
      <td>7/17/2016</td>
      <td>Beach</td>
    </tr>
    <tr>
      <th>18</th>
      <td>7/18/2016</td>
      <td>Park</td>
    </tr>
    <tr>
      <th>19</th>
      <td>7/19/2016</td>
      <td>Park</td>
    </tr>
    <tr>
      <th>22</th>
      <td>7/22/2016</td>
      <td>Park</td>
    </tr>
    <tr>
      <th>23</th>
      <td>7/23/2016</td>
      <td>Park</td>
    </tr>
    <tr>
      <th>24</th>
      <td>7/24/2016</td>
      <td>Park</td>
    </tr>
    <tr>
      <th>25</th>
      <td>7/25/2016</td>
      <td>Park</td>
    </tr>
    <tr>
      <th>26</th>
      <td>7/26/2016</td>
      <td>Park</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-80c7ea4c-f3b6-416c-90a6-935ca4d10c87')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-80c7ea4c-f3b6-416c-90a6-935ca4d10c87 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-80c7ea4c-f3b6-416c-90a6-935ca4d10c87');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
juice.iloc[juice['Leaflets'] >= 100, 0:2]
```

## 정렬
- sort_values()


```python
# 매출액 순서로 정렬
juice.sort_values(by=['Revenue'], ascending=False).head(3) 
```





  <div id="df-d4ef77c6-8bab-4eae-9f75-40bfaf70f3b7">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Location</th>
      <th>Lemon</th>
      <th>Orange</th>
      <th>Temperature</th>
      <th>Leaflets</th>
      <th>Price</th>
      <th>Sold</th>
      <th>Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>25</th>
      <td>7/25/2016</td>
      <td>Park</td>
      <td>156</td>
      <td>113</td>
      <td>84</td>
      <td>135.0</td>
      <td>0.50</td>
      <td>269</td>
      <td>134.50</td>
    </tr>
    <tr>
      <th>18</th>
      <td>7/18/2016</td>
      <td>Park</td>
      <td>131</td>
      <td>92</td>
      <td>81</td>
      <td>122.0</td>
      <td>0.50</td>
      <td>223</td>
      <td>111.50</td>
    </tr>
    <tr>
      <th>26</th>
      <td>7/26/2016</td>
      <td>Park</td>
      <td>176</td>
      <td>129</td>
      <td>83</td>
      <td>158.0</td>
      <td>0.35</td>
      <td>305</td>
      <td>106.75</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-d4ef77c6-8bab-4eae-9f75-40bfaf70f3b7')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-d4ef77c6-8bab-4eae-9f75-40bfaf70f3b7 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-d4ef77c6-8bab-4eae-9f75-40bfaf70f3b7');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
# 2개 이상 기준으로 할 경우, 그룹화하여 정렬됨
juice.sort_values(by=['Price', 'Temperature'], ascending=False) 

#이것도 가능
#juice.sort_values(by=['Price', 'Temperature'], ascending=[False, True]) -> Price는 내림차순, Temparature는 오름차순
#juice.sort_values(by=['Price', 'Temperature'], ascending=[False, True]).rest_index(drop=True)  -> index 번호도 재정렬
```





  <div id="df-14051fd5-627b-4ebe-ab05-3415f55cc7f3">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Location</th>
      <th>Lemon</th>
      <th>Orange</th>
      <th>Temperature</th>
      <th>Leaflets</th>
      <th>Price</th>
      <th>Sold</th>
      <th>Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>25</th>
      <td>7/25/2016</td>
      <td>Park</td>
      <td>156</td>
      <td>113</td>
      <td>84</td>
      <td>135.0</td>
      <td>0.50</td>
      <td>269</td>
      <td>134.50</td>
    </tr>
    <tr>
      <th>24</th>
      <td>7/24/2016</td>
      <td>Park</td>
      <td>121</td>
      <td>82</td>
      <td>82</td>
      <td>117.0</td>
      <td>0.50</td>
      <td>203</td>
      <td>101.50</td>
    </tr>
    <tr>
      <th>18</th>
      <td>7/18/2016</td>
      <td>Park</td>
      <td>131</td>
      <td>92</td>
      <td>81</td>
      <td>122.0</td>
      <td>0.50</td>
      <td>223</td>
      <td>111.50</td>
    </tr>
    <tr>
      <th>23</th>
      <td>7/23/2016</td>
      <td>Park</td>
      <td>120</td>
      <td>82</td>
      <td>81</td>
      <td>117.0</td>
      <td>0.50</td>
      <td>202</td>
      <td>101.00</td>
    </tr>
    <tr>
      <th>22</th>
      <td>7/22/2016</td>
      <td>Park</td>
      <td>112</td>
      <td>75</td>
      <td>80</td>
      <td>108.0</td>
      <td>0.50</td>
      <td>187</td>
      <td>93.50</td>
    </tr>
    <tr>
      <th>19</th>
      <td>7/19/2016</td>
      <td>Park</td>
      <td>122</td>
      <td>85</td>
      <td>78</td>
      <td>113.0</td>
      <td>0.50</td>
      <td>207</td>
      <td>103.50</td>
    </tr>
    <tr>
      <th>17</th>
      <td>7/17/2016</td>
      <td>Beach</td>
      <td>115</td>
      <td>76</td>
      <td>77</td>
      <td>126.0</td>
      <td>0.50</td>
      <td>191</td>
      <td>95.50</td>
    </tr>
    <tr>
      <th>21</th>
      <td>7/21/2016</td>
      <td>Park</td>
      <td>83</td>
      <td>50</td>
      <td>77</td>
      <td>90.0</td>
      <td>0.50</td>
      <td>133</td>
      <td>66.50</td>
    </tr>
    <tr>
      <th>15</th>
      <td>7/15/2016</td>
      <td>Beach</td>
      <td>98</td>
      <td>62</td>
      <td>75</td>
      <td>108.0</td>
      <td>0.50</td>
      <td>160</td>
      <td>80.00</td>
    </tr>
    <tr>
      <th>16</th>
      <td>7/16/2016</td>
      <td>Beach</td>
      <td>81</td>
      <td>50</td>
      <td>74</td>
      <td>90.0</td>
      <td>0.50</td>
      <td>131</td>
      <td>65.50</td>
    </tr>
    <tr>
      <th>20</th>
      <td>7/20/2016</td>
      <td>Park</td>
      <td>71</td>
      <td>42</td>
      <td>70</td>
      <td>NaN</td>
      <td>0.50</td>
      <td>113</td>
      <td>56.50</td>
    </tr>
    <tr>
      <th>26</th>
      <td>7/26/2016</td>
      <td>Park</td>
      <td>176</td>
      <td>129</td>
      <td>83</td>
      <td>158.0</td>
      <td>0.35</td>
      <td>305</td>
      <td>106.75</td>
    </tr>
    <tr>
      <th>28</th>
      <td>7/28/2016</td>
      <td>Park</td>
      <td>96</td>
      <td>63</td>
      <td>82</td>
      <td>90.0</td>
      <td>0.35</td>
      <td>159</td>
      <td>55.65</td>
    </tr>
    <tr>
      <th>30</th>
      <td>7/30/2016</td>
      <td>Beach</td>
      <td>88</td>
      <td>57</td>
      <td>82</td>
      <td>81.0</td>
      <td>0.35</td>
      <td>145</td>
      <td>50.75</td>
    </tr>
    <tr>
      <th>31</th>
      <td>7/31/2016</td>
      <td>Beach</td>
      <td>76</td>
      <td>47</td>
      <td>82</td>
      <td>68.0</td>
      <td>0.35</td>
      <td>123</td>
      <td>43.05</td>
    </tr>
    <tr>
      <th>29</th>
      <td>7/29/2016</td>
      <td>Park</td>
      <td>100</td>
      <td>66</td>
      <td>81</td>
      <td>95.0</td>
      <td>0.35</td>
      <td>166</td>
      <td>58.10</td>
    </tr>
    <tr>
      <th>27</th>
      <td>7/27/2016</td>
      <td>Park</td>
      <td>104</td>
      <td>68</td>
      <td>80</td>
      <td>99.0</td>
      <td>0.35</td>
      <td>172</td>
      <td>60.20</td>
    </tr>
    <tr>
      <th>12</th>
      <td>7/12/2016</td>
      <td>Beach</td>
      <td>130</td>
      <td>95</td>
      <td>84</td>
      <td>99.0</td>
      <td>0.25</td>
      <td>225</td>
      <td>56.25</td>
    </tr>
    <tr>
      <th>11</th>
      <td>7/11/2016</td>
      <td>Beach</td>
      <td>162</td>
      <td>120</td>
      <td>83</td>
      <td>135.0</td>
      <td>0.25</td>
      <td>282</td>
      <td>70.50</td>
    </tr>
    <tr>
      <th>5</th>
      <td>7/6/2016</td>
      <td>Beach</td>
      <td>103</td>
      <td>69</td>
      <td>82</td>
      <td>90.0</td>
      <td>0.25</td>
      <td>172</td>
      <td>43.00</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7/6/2016</td>
      <td>Beach</td>
      <td>103</td>
      <td>69</td>
      <td>82</td>
      <td>90.0</td>
      <td>0.25</td>
      <td>172</td>
      <td>43.00</td>
    </tr>
    <tr>
      <th>8</th>
      <td>NaN</td>
      <td>Beach</td>
      <td>123</td>
      <td>86</td>
      <td>82</td>
      <td>113.0</td>
      <td>0.25</td>
      <td>209</td>
      <td>52.25</td>
    </tr>
    <tr>
      <th>10</th>
      <td>7/10/2016</td>
      <td>Beach</td>
      <td>140</td>
      <td>98</td>
      <td>82</td>
      <td>131.0</td>
      <td>0.25</td>
      <td>238</td>
      <td>59.50</td>
    </tr>
    <tr>
      <th>7</th>
      <td>7/7/2016</td>
      <td>Beach</td>
      <td>143</td>
      <td>101</td>
      <td>81</td>
      <td>135.0</td>
      <td>0.25</td>
      <td>244</td>
      <td>61.00</td>
    </tr>
    <tr>
      <th>9</th>
      <td>7/9/2016</td>
      <td>Beach</td>
      <td>134</td>
      <td>95</td>
      <td>80</td>
      <td>126.0</td>
      <td>0.25</td>
      <td>229</td>
      <td>57.25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>7/5/2016</td>
      <td>Beach</td>
      <td>159</td>
      <td>118</td>
      <td>78</td>
      <td>135.0</td>
      <td>0.25</td>
      <td>277</td>
      <td>69.25</td>
    </tr>
    <tr>
      <th>14</th>
      <td>7/14/2016</td>
      <td>Beach</td>
      <td>122</td>
      <td>85</td>
      <td>78</td>
      <td>113.0</td>
      <td>0.25</td>
      <td>207</td>
      <td>51.75</td>
    </tr>
    <tr>
      <th>13</th>
      <td>7/13/2016</td>
      <td>Beach</td>
      <td>109</td>
      <td>75</td>
      <td>77</td>
      <td>99.0</td>
      <td>0.25</td>
      <td>184</td>
      <td>46.00</td>
    </tr>
    <tr>
      <th>3</th>
      <td>7/4/2016</td>
      <td>Beach</td>
      <td>134</td>
      <td>99</td>
      <td>76</td>
      <td>98.0</td>
      <td>0.25</td>
      <td>233</td>
      <td>58.25</td>
    </tr>
    <tr>
      <th>1</th>
      <td>7/2/2016</td>
      <td>Park</td>
      <td>98</td>
      <td>67</td>
      <td>72</td>
      <td>90.0</td>
      <td>0.25</td>
      <td>165</td>
      <td>41.25</td>
    </tr>
    <tr>
      <th>2</th>
      <td>7/3/2016</td>
      <td>Park</td>
      <td>110</td>
      <td>77</td>
      <td>71</td>
      <td>104.0</td>
      <td>0.25</td>
      <td>187</td>
      <td>46.75</td>
    </tr>
    <tr>
      <th>0</th>
      <td>7/1/2016</td>
      <td>Park</td>
      <td>97</td>
      <td>67</td>
      <td>70</td>
      <td>90.0</td>
      <td>0.25</td>
      <td>164</td>
      <td>41.00</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-14051fd5-627b-4ebe-ab05-3415f55cc7f3')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-14051fd5-627b-4ebe-ab05-3415f55cc7f3 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-14051fd5-627b-4ebe-ab05-3415f55cc7f3');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




### Group by
- R dplyr groupby() %>% summarize()
- -> 데이터 요약 -> 엑셀로 피벗 테이블


```python
# Location 항목을 카운트
juice.groupby(by = 'Location').count()  
```





  <div id="df-26afeca1-6bb7-494f-ba2d-92aab015b058">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Lemon</th>
      <th>Orange</th>
      <th>Temperature</th>
      <th>Leaflets</th>
      <th>Price</th>
      <th>Sold</th>
      <th>Revenue</th>
    </tr>
    <tr>
      <th>Location</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Beach</th>
      <td>16</td>
      <td>17</td>
      <td>17</td>
      <td>17</td>
      <td>17</td>
      <td>17</td>
      <td>17</td>
      <td>17</td>
    </tr>
    <tr>
      <th>Park</th>
      <td>15</td>
      <td>15</td>
      <td>15</td>
      <td>15</td>
      <td>14</td>
      <td>15</td>
      <td>15</td>
      <td>15</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-26afeca1-6bb7-494f-ba2d-92aab015b058')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-26afeca1-6bb7-494f-ba2d-92aab015b058 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-26afeca1-6bb7-494f-ba2d-92aab015b058');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
# 집계 함수
import numpy as np

juice.groupby(['Location'])['Revenue'].agg([max, min, sum, np.mean])  
```





  <div id="df-650575f1-c764-4097-b860-3fa1b26021c5">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>max</th>
      <th>min</th>
      <th>sum</th>
      <th>mean</th>
    </tr>
    <tr>
      <th>Location</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Beach</th>
      <td>95.5</td>
      <td>43.0</td>
      <td>1002.8</td>
      <td>58.988235</td>
    </tr>
    <tr>
      <th>Park</th>
      <td>134.5</td>
      <td>41.0</td>
      <td>1178.2</td>
      <td>78.546667</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-650575f1-c764-4097-b860-3fa1b26021c5')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-650575f1-c764-4097-b860-3fa1b26021c5 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-650575f1-c764-4097-b860-3fa1b26021c5');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
# 집계 함수
import numpy as np

juice.groupby(['Location'])['Revenue', 'Lemon'].agg([max, min, sum, np.mean])  
```

    /usr/local/lib/python3.7/dist-packages/ipykernel_launcher.py:4: FutureWarning: Indexing with multiple keys (implicitly converted to a tuple of keys) will be deprecated, use a list instead.
      after removing the cwd from sys.path.
    





  <div id="df-7a3b6989-de2d-4a76-8bd8-66538dc5863c">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="4" halign="left">Revenue</th>
      <th colspan="4" halign="left">Lemon</th>
    </tr>
    <tr>
      <th></th>
      <th>max</th>
      <th>min</th>
      <th>sum</th>
      <th>mean</th>
      <th>max</th>
      <th>min</th>
      <th>sum</th>
      <th>mean</th>
    </tr>
    <tr>
      <th>Location</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Beach</th>
      <td>95.5</td>
      <td>43.0</td>
      <td>1002.8</td>
      <td>58.988235</td>
      <td>162</td>
      <td>76</td>
      <td>2020</td>
      <td>118.823529</td>
    </tr>
    <tr>
      <th>Park</th>
      <td>134.5</td>
      <td>41.0</td>
      <td>1178.2</td>
      <td>78.546667</td>
      <td>176</td>
      <td>71</td>
      <td>1697</td>
      <td>113.133333</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-7a3b6989-de2d-4a76-8bd8-66538dc5863c')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-7a3b6989-de2d-4a76-8bd8-66538dc5863c button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-7a3b6989-de2d-4a76-8bd8-66538dc5863c');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>



