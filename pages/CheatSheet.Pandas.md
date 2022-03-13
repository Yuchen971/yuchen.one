- {{renderer :tocgen}}
- **Rows**
collapsed:: true
	- **去掉只出现一次的行**
collapsed:: true
		- ```python
		  df[df.groupby('x').x.transform(len) > 1]
		  ```
- **Columns**
collapsed:: true
	- **合并两列为新的一列**
collapsed:: true
		- ```python
		  df['date'] = df['年'].map(str)+"/"+df['月'].map(str)+"/"+df['日'].map(str)
		  ```
- **Date**
collapsed:: true
	- **找出连续日期**
collapsed:: true
		- ```python
		  # 连续日期
		  df['date'] = pd.to_datetime(df['date'])
		  dt = df['date']
		  day = pd.Timedelta('1d')
		  in_block = ((dt - dt.shift(-1)).abs() == day) | (dt.diff() == day)
		  filt = df.loc[in_block]
		  breaks = filt['date'].diff() != day
		  groups = breaks.cumsum()
		  
		  for _, frame in filt.groupby(groups):
		      print(frame['20-20时累计降水量(0.1mm)'], end='\n\n')
		  
		  #单独日期：
		  dt = df['date']
		  day = pd.Timedelta('1d')
		  in_block = ((dt - dt.shift(-1)).abs() == day) | (dt.diff() == day)
		  breaks = dt.diff() != day
		  groups = breaks.cumsum()
		  ```
		- [python – 在Pandas DataFrame中查找连续日期组](https://www.icode9.com/content-1-493830.html)
	- **日期转置合并**
collapsed:: true
		- ```python
		  city_list = ['北京市','天津市','河北省','山西省','内蒙古自治区',
		               '辽宁省','吉林省','黑龙江省','上海市','江苏省','浙江省',
		               '安徽省','福建省','江西省','山东省','河南省','湖北省','湖南省',
		               '广东省','广西壮族自治区','海南省','四川省','贵州省','云南省',
		               '西藏自治区','陕西省','甘肃省','青海省','宁夏回族自治区','新疆维吾尔自治区',]
		  
		  date_list = ['1995', '1996', '1997', '1998', '1999', '2000', '2001', '2002', '2003',
		         '2004', '2005', '2006', '2007', '2008', '2009', '2010', '2011', '2012',
		         '2013', '2014', '2015', '2016', '2017', '2018', '2019']
		  # 根据省份名称groupby
		  dictionary = dict(list(房屋施工面积.groupby('省份名称')))
		  # 时间和城市的空dataframe
		  finaldf = pd.DataFrame(columns = date_list, index = city_list)
		  # 空dataframe里面添加groupby数据
		  # 其中.values(x) x是第几行数据 可以打印出来看一下
		  for city in city_list:
		    for date in date_list:
		      finaldf[date][city] = dictionary[city].set_index('年度标识').loc[int(date)].values[1]
		  ```
- **Index**
collapsed:: true
	- **反向索引**
collapsed:: true
		- ```python
		  df[~df.index.isin(last_multiple_days_date)]
		  ```
- **Others**
collapsed:: true
	- **双向interpolate**
collapsed:: true
		- ```python
		  # 如果单向interpolate，在首位的NaN值会保留，必须双向interpolate
		  pd.interpolate(limit_direction='both')
		  ```
	- **CSV中文乱码**
collapsed:: true
		- ```python
		  import pandas as pd
		  import os
		  fileList = os.listdir('/content/Untitled Folder')
		  for i in fileList:
		    if i[-4:] == '.csv':
		      temp = pd.read_csv(f'/content/Untitled Folder/{i}',encoding='gbk')
		      temp.to_excel(f'/content/{i[:-4]}.xlsx')
		  或者 utf_8_sig
		  ```