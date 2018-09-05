
# Industry 4.0 의 중심, BigData

<div align='right'><font size=2 color='gray'>Data Processing Based Python @ <font color='blue'><a href='https://www.facebook.com/jskim.kr'>FB / jskim.kr</a></font>, [김진수](bigpycraft@gmail.com)</font></div>
<hr>

## Date, Time 

### <font color='brown'>시간 정보</font>


```python
# 현재 시간을 년-월-일 시:분:초로 출력하기(localtime, strftime)
from time import localtime, strftime

def writelog(logfile, log):
    time_stamp = strftime('%Y-%m-%d %X\t', localtime())
    log = time_stamp + log + '\n'

    with open(logfile, 'a') as f:
        f.writelines(log)

logfile = 'test.log'
writelog(logfile, '첫번째 로깅 문장입니다.')

```


```python
! cat test.log
```

    'cat'은(는) 내부 또는 외부 명령, 실행할 수 있는 프로그램, 또는
    배치 파일이 아닙니다.
    


```python
# 올해 경과된 날짜수 계산하기(localtime)
from time import localtime

t = localtime()
# print(t)

start_day = '%d-01-01' % (t.tm_year)
elapsed_day = t.tm_yday

print('오늘은 [%s]이후 [%d]일째 되는 날입니다.' %(start_day, elapsed_day))

```

    오늘은 [2018-01-01]이후 [245]일째 되는 날입니다.
    


```python
today = '{yy}-{mm}-{dd}'.format(
    yy = t.tm_year,
    mm = t.tm_mon,
    dd = t.tm_mday,
)
today
```




    '2018-9-2'




```python
mem_day = '{yy}-{mm}-{dd}'.format(
    yy = 2014,
    mm = 4,
    dd = 16
)
mem_day
```




    '2014-4-16'




```python
type(t)
```




    time.struct_time




```python
# 오늘의 요일 계산하기(localtime)
from time import localtime

weekdays = ['월요일', '화요일', '수요일', '목요일', '금요일', '토요일', '일요일']

t = localtime()
today = '%d-%d-%d' %(t.tm_year, t.tm_mon, t.tm_mday)
week = weekdays[t.tm_wday]

print('[%s] 오늘은 [%s]입니다.' %(today, week))

```

    [2018-9-2] 오늘은 [일요일]입니다.
    


```python
# 프로그램 실행 시간 계산하기(datetimenow)
from datetime import datetime, timedelta

start = datetime.now()
print('1에서 백만까지 더합니다.')

ret = 0
for i in range(1000000):
    ret += i

print('1에서 백만까지 더한 결과: %d' %ret)
end = datetime.now()

elapsed = end - start
print('총 계산 시간: ', end='');   print(elapsed)
elapsed_ms = int(elapsed.total_seconds()*1000)
print('총 계산 시간: %dms' %elapsed_ms)

```

    1에서 백만까지 더합니다.
    1에서 백만까지 더한 결과: 499999500000
    총 계산 시간: 0:00:00.139105
    총 계산 시간: 139ms
    


```python
type(start)
```




    datetime.datetime




```python
from datetime import datetime
 
now = datetime.now()
print(now)          # yyyy-MM-dd hh:mm:ss
 
nowDate = now.strftime('%Y-%m-%d')
print(nowDate)      # yyyy-MM-dd 
 
nowTime = now.strftime('%H:%M:%S')
print(nowTime)      # 1hh:mm:ss
 
nowDatetime = now.strftime('%Y-%m-%d %H:%M:%S')
print(nowDatetime)  # yyyy-MM-dd hh:mm:ss
```

    2018-09-02 06:00:38.458011
    2018-09-02
    06:00:38
    2018-09-02 06:00:38
    


```python
type(now)
```




    datetime.datetime




```python
m_day = datetime(2002, 3, 2)
m_day
```




    datetime.datetime(2002, 3, 2, 0, 0)




```python
today = datetime.now()
today
```




    datetime.datetime(2018, 9, 2, 6, 0, 38, 503040)




```python
elapsed = today - m_day
elapsed
```




    datetime.timedelta(6028, 21638, 503040)




```python
elapsed.days, elapsed.seconds, elapsed.microseconds
```




    (6028, 21638, 503040)




```python
elapsed_day   = elapsed.days
elapsed_month = elapsed_day / 30
elapsed_year  = elapsed_day / 365

'오늘은 기념일로부터 {e_dd}일 경과되었고, 월수는 {e_mm}개월, 년수는 {e_yy}년이 지났군요!!'.format(
    e_dd = elapsed_day,
    e_mm = int(elapsed_month),
    e_yy = int(elapsed_year)
)
```




    '오늘은 기념일로부터 6028일 경과되었고, 월수는 200개월, 년수는 16년이 지났군요!!'




```python
from datetime import datetime

def getMemorialDay(year, month, day, mem_day='기념일', is_msg=True):
    m_day = datetime(year, month, day)
    today = datetime.now()
    elapsed = today - m_day

    elapsed_day   = elapsed.days
    elapsed_month = int(elapsed_day / 30)
    elapsed_year  = int(elapsed_day /365)

    msg = '오늘은 "{mday}"로부터 {e_dd}일 경과되었고, 달 수로는 {e_mm}개월째, 연 수로는 {e_yy}년째 되었습니다!!'.format(
        mday = mem_day,
        e_dd = elapsed_day,
        e_mm = elapsed_month,
        e_yy = elapsed_year
    )
    if is_msg: print(msg)
        
    return elapsed_year, elapsed_month, elapsed_day
```


```python
getMemorialDay(2014,4,16, '세월호침몰사고일')
```

    오늘은 "세월호침몰사고일"로부터 1600일 경과되었고, 달 수로는 53개월째, 연 수로는 4년째 되었습니다!!
    




    (4, 53, 1600)




```python
_y, _m, elapsed_day = getMemorialDay(2018, 12, 25, '크리스마스', False)
'크리스마스까지는 %d일 남았습니다!!' % -elapsed_day

```




    '크리스마스까지는 114일 남았습니다!!'




```python
# 주어진 숫자를 천 단위로 구분하기
num = input('아무 숫자를 입력하세요: ')

if num.isdigit():
    num = num[::-1]
    ret = ''
    for i, c in enumerate(num):
        i += 1
        if i != len(num) and i%3 == 0:
            ret += (c + ',')
        else:
            ret += c
    ret = ret[::-1]
    print(ret)
else:
    print('입력한 내용 [%s]: 숫자가 아닙니다.' %num)
```

    아무 숫자를 입력하세요: 1234567890
    1,234,567,890
    

<hr>
<marquee><font size=3 color='brown'>The BigpyCraft find the information to design valuable society with Technology & Craft.</font></marquee>
<div align='right'><font size=2 color='gray'> &lt; The End &gt; </font></div>
