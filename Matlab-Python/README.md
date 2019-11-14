
# [Python + MATLAB](https://kr.mathworks.com/help/matlab/matlab-engine-for-python.html)

Python에서 matlab코드 호출 하는 2가지 방법 
- MATLAB Engine API : 매틀랩 설치 필요 
- Compiled Python Package : 매틀랩 설치 불 필요 


## 1. MATLAB Engine API

### 1.1 엔진 설치 

```python 
$ cd /usr/local/MATLAB/R2019b/extern/engines/python
$ sudo python setup.py install --user
```




### 1.2 활용 


in Python 

```python 
import matlab.engine

#Start MATLAB 
eng = matlab.engine.start_matlab()

...

#Stop MATLAB
eng.quit()


```


## 2. Compiled Python Package


in MATLAB

- Apps -> libraty compiler -> type: python package -> Select `code.m`

> [Calling MATLAB from Python](https://kr.mathworks.com/products/matlab/matlab-and-python.html?fbclid=IwAR3Zd9shiPzSEHlOrtOGzpUY4ssOVz03rFD3dkbjWt944hfX0nKFy6796fs)


in Python 

```python 
import `생성된 패키지 명`

```





---



# MATLAB + Python 


