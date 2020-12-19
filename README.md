# hello-world
just another repository
import csv
from datetime import datetime

from matplotlib import pyplot as plt

filename='F:\py学习\《Python编程》源代码文件-更新\《Python编程》源代码文件\chapter_16' \
         '\death_valley_2014.csv'
with open(filename) as f:
    reader=csv.reader(f)
    header_row=next(reader)

    dates,highs,lows=[],[],[]

    for row in reader:
        try:
            current_date=datetime.strptime(row[0],"%Y-%m-%d")
            high=int(row[1])
            low=int(row[3])
        except:
            print(current_date,' missing data')
        else:
            dates.append(current_date)
            highs.append(high)
            lows.append(low)

    print(highs)
#根据数据绘制图形
fig=plt.figure(dpi=128,figsize=(10,6))
plt.plot(dates,highs,c="red",alpha=0.5)
plt.plot(dates,lows,c="blue",alpha=0.5)
plt.fill_between(dates,lows,highs,facecolor='blue',alpha=0.1)
#为图形设置标签
plt.title("daily high and low temperatures - 2014 of 1 ",
          fontsize=16)
plt.xlabel(' ',fontsize=16)
fig.autofmt_xdate()
plt.ylabel('temperature',fontsize=16)
plt.tick_params(axis='both',which='major',labelsize=16)
plt.show()
