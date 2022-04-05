- {{renderer :tocgen,[[]],2}}
-
- **String**
	- **去掉字符串空格**
	  collapsed:: true
		- ```python
		  ''.join(i.split())
		  ```
	- **Str转Float**
	  collapsed:: true
		- ```python
		  weight_list['mv_es'] = pd.to_numeric(weight_list['mv_es'])
		  # float -> str
		  list(map(str,年末总人口.columns))
		  ```
	- **f-string**
	  collapsed:: true
		- ```python
		  name = 'Peter'
		  age = 23
		  people = 3
		  print(f'{name} is {age} years old')
		  print(f'total age is {age * people}')
		  # f-string format floats
		  val = 12.3
		  print(f'{val:.2f}')
		  print(f'{val:.5f}')
		  # f-string numeric notations
		  a = 300
		  print(f'{a:e}')
		  # multiline f-string
		  name = 'John Doe'
		  age = 32
		  occupation = 'gardener'
		  msg = (
		      f'Name: {name}\n'
		      f'Age: {age}\n'
		      f'Occupation: {occupation}'
		  )
		  # f-string format datetime
		  now = datetime.datetime.now()
		  print(f'{now:%Y-%m-%d %H:%M}')
		  ```
- **List**
	- **打开嵌套列表**
	  collapsed:: true
		- ```python
		  # Way 1:
		  [n for a in target_list for n in a]#两层列表
		  # Way 2:
		  sum(target_list,[])
		  ```
	- **取出list重复数据并列出次数**
	  collapsed:: true
		- ```python
		  from collections import Counter #引入Counter
		  a = 面板数据.index
		  b = dict(Counter(a))
		  print([key for key,value in b.items()if value > 1]) #只展示重复元素
		  print({key:value for key,value in b.items()if value > 9}) #展现重复元素和重复次数
		  ```
	- **list中检测含有某个类**
	  collapsed:: true
		- ```python
		  any(isinstance(x, target_class) for x in target_list)
		  ```
	- **两个list取交集**
	  collapsed:: true
		- ```python
		  list(set(lstA).intersection(set(lstB)))
		  ```
	- **list分组**
	  collapsed:: true
		- ```python
		  a = [1,2,3,4,5,6,7,8,9,10,11]
		  step = 3
		  b = [a[i:i+step] for i in range(0,len(a),step)]
		  ```
- **Dict**
	- **创建空列表的字典**
	  collapsed:: true
		- ```python
		  key = [1, 2, 3, 4]
		  a = dict([(k,[]) for k in key])
		  
		  {1: [], 2: [], 3: [], 4: []}
		  ```
	- **字典删除多个key**
	  collapsed:: true
		- ```python
		  myDict = {'a': 1, 'b': 2, 'c': 3, 'd': 4}
		  map(myDict.pop, ['a', 'c'])
		  ```
	- **字典排序**
	  collapsed:: true
		- ```python
		  # want to sort dicts like this
		  '''
		  d = [{'name': '广东', 'value': 72812.55},
		   {'name': '江苏', 'value': 70116.38},
		   {'name': '山东', 'value': 63002.3},
		   {'name': '浙江', 'value': 42886},
		   {'name': '河南', 'value': 37010.25},
		   {'name': '台湾', 'value': 32604.52},
		   {'name': '四川', 'value': 30103.1},
		   {'name': '河北', 'value': 29806.1},
		   {'name': '湖北', 'value': 29550.19},
		   {'name': '湖南', 'value': 29047.2}]
		  '''
		  import operator
		  d.sort(key=operator.itemgetter('value'),reverse=True)
		  #默认为升序， reverse=True为降序
		  
		  或者:
		  d={'a':1,'c':3,'b':2}    # 首先建一个字典d
		  #d.items()返回的是： dict_items([('a', 1), ('c', 3), ('b', 2)])
		  d_order=sorted(d.items(),key=lambda x:x[1],reverse=False)
		  '''
		  sorted高阶函数语法格式：  sorted(可迭代对象,key=函数名,reverse=False/True)
		       作用：从可迭代对象中，依次取出一个元素，该元素再按照key规定的排列依据排序。
		       可迭代对象：即可依次取值的对象，例如：集合，序列（列表，字符串，元组），字典等。
		       key : 是列表排列的依据，一般可以自定义一个函数返回排序的依据，再把函数名绑定给key。
		       reverse : 译为反转，reverse默认等于False，从小到大排序。等于True时，从大到小排序。
		  '''
		  ```
- **Excel related**
	- **Excel表分割**
	  collapsed:: true
		- ```python
		  !pip install xlsxwriter
		  import pandas as pd
		  import xlsxwriter
		  data = pd.read_excel('/content/luanxu.xls', header = None)
		  writer = pd.ExcelWriter('/content/luanxu.xlsx', engine='xlsxwriter')
		  # divide the Excel by 100 per sheet
		  for i in range(80): # data has 7965 rows
		    if i == 0:
		      df = data.iloc[:100,:]
		      df.to_excel(writer, sheet_name = 'day{}'.format(i+1), index = False)
		    else:
		      df = data.iloc[i*100:(i+1)*100,:]
		      df.to_excel(writer, sheet_name = 'day{}'.format(i+1), index = False)
		      
		  writer.save()
		  ```
	- **Excel 链接转图片方法**
	  collapsed:: true
		- [Excel技巧，如何批量快速将图片链接转换为图片](https://www.nofuwb.com/2021/04/11/linktoimage/)
		- ```
		  1. 辅助列其中C2为表格中图片地址的单元格位置
		  ="<table><img src="&C2&" height=50 width=50></table>"
		  2. 调整放置单元格的大小
		  3. 将步骤1中生成的地址复制到记事本, 然后将记事本中的代码复制到存放图片的位置
		  4. 选中所有图片, 右键, 大小和属性, 调整图片大小
		  ```
- **Other**
	- **批量命名变量并批量调用**
	  collapsed:: true
		- ```python
		  # 需要对不同城市创建不同城市名称的线性模型
		  province_list = ['北京市','天津市','河北省','山西省','内蒙古自治区',
		               '辽宁省','吉林省','黑龙江省','上海市','江苏省','浙江省',
		               '安徽省','福建省','江西省','山东省','河南省','湖北省','湖南省',
		               '广东省','广西壮族自治区','海南省','四川省','贵州省','云南省',
		               '西藏自治区','陕西省','甘肃省','青海省','宁夏回族自治区','新疆维吾尔自治区',]
		  
		  coef = []
		  fig = go.Figure()
		  # 使用createVar
		  createVar = locals()
		  for i in province_list:
		    X = 城镇化率.loc[i].values.reshape(-1, 1)
		    y = 一般预算支出.loc[i]
		    X_train, X_test, y_train, y_test = train_test_split(X, y, random_state=0)
		  
		    # 创建不同城市线性模型，并且使用temp代替每次的动态变量名称
		    createVar['model_'+ str(i)] = LinearRegression().fit(X_train, y_train)
		    exec(f'temp = model_{i}')
		    temp=locals()['temp']
		    x_range = np.linspace(X.min(), X.max(), 100)
		    y_range = temp.predict(x_range.reshape(-1, 1))
		    #print(f'{i}斜率为{model.coef_}')
		    coef.append(temp.coef_)
		  
		    fig.add_traces([
		        go.Scatter(x=X.squeeze(), y=y, name=i, mode='markers',opacity=0.6,marker=dict(color = colors.loc[i])),
		        #go.Scatter(x=X_test.squeeze(), y=y_test, name='test', mode='markers'),
		        go.Scatter(x=x_range, y=y_range, name=f'{i}_prediction',marker=dict(color = colors['2005'][i])),
		    ])
		  
		    from sklearn import metrics
		    y_pred = temp.predict(X_test)
		    print(f"{i}prediction的R2为:{metrics.r2_score(y_test, y_pred)*100:.1f}%")
		  
		  fig.update_layout(
		      title="城镇化率 vs 一般预算支出",
		      xaxis_title="城镇化率",
		      yaxis_title="一般预算支出",
		      font = dict(size = 15)
		      #legend_title="Legend Title",
		  )
		  
		  fig.show()
		  ```