
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

- 기본 구조 
    
    ```python 
    import matlab.engine
    
    #Start MATLAB 
    eng = matlab.engine.start_matlab()
    
    #Run MATLAB Function 
    
    #Stop MATLAB
    eng.quit()
    ```

- [MATLAB함수에 데이터 전달](https://kr.mathworks.com/help/matlab/matlab_external/matlab-arrays-as-python-variables.html) : list, numpy는 인식 못함, MATLAB 으로 변경 필요 

    ```python 
    # a = np.asarray([1,4,9,16,25]) #에러 
    # a = [1,4,9,16,25] #에러 
    a = matlab.double([1,4,9,16,25])
    b = eng.sqrt(a)
    print(b, b.size)
    
    # 단, MATLAB 결과물은 바로 사용 가능 
    
    ```
    
    ```python 
    def npArray2Matlab(x):
        return matlab.double(x.tolist())
    ```



    
    > [조심] [Python 데이터형과 MATLAB 스칼라 유형 간의 변환 규칙](https://kr.mathworks.com/help/matlab/matlab_external/pass-data-to-matlab-from-python.html), [MATLAB 스칼라 유형과 Python 데이터형 간 매핑](https://kr.mathworks.com/help/matlab/matlab_external/handle-data-returned-from-matlab-to-python.html)
    

- [Python에서 MATLAB 함수 호출하기](https://kr.mathworks.com/help/matlab/matlab_external/call-matlab-functions-from-python.html)

    > 동일 폴더내 파일(triarea.m) 존재시 별도 import 동작 없이 사용 가능  :`eng.triarea(nargout=0)`
    
    ```python 
    tf = eng.isprime(37, nargout=1) #[중요] 출력 인자 수를 `nartout`으로 지정 하여야 함 
    print(tf)
    
    ```

- [Call MATLAB Functions Asynchronously from Python](https://kr.mathworks.com/help/matlab/matlab_external/call-matlab-functions-asynchronously-from-python.html) 

    > 동작 완료후 값 반환, 동작 중 python 실행 가능 
    
    ```python
    # Use the background argument to call a MATLAB function asynchronously.
    
    import matlab.engine
    eng = matlab.engine.start_matlab()
    future = eng.sqrt(4.0,background=True)
    ret = future.result()
    print(ret)
    
    #To stop execution of the function before it finishes, call future.cancel().
    ```
    


### 1.3 팁

#### 도움말 

- 도울말 창 : `eng.doc(nargout=0)`
- 도움말 출력 : `eng.doc("plot",nargout=0)` OR `eng.help("erf",nargout=0)`
- 도움말 찾기 : `eng.docsearch("plot",nargout=0)`


### mat파일 읽기 

    ```python 
    from scipy import io
    
    mat_file = io.loadmat('data.mat')
    
    #OR
    eng = matlab.engine.start_matlab()
    mat_file = eng.load('data.mat')
    
    
    result = mat_file.values()
    ```

#### [값 공유](https://kr.mathworks.com/help/matlab/matlab_external/use-the-matlab-engine-workspace-in-python.html)

```python 
import matlab.engine
eng = matlab.engine.start_matlab()

x = 4.0
eng.workspace['y'] = x
a = eng.eval('sqrt(y)')
print(a)

```

- [Use MATLAB Handle Objects in Python](https://kr.mathworks.com/help/matlab/matlab_external/use-matlab-handle-objects-in-python.html)


#### 세션 공유 

> [로컬 컴퓨터에서 이미 실행 중인 공유 MATLAB® 세션에 Python®용 MATLAB 엔진을 연결](https://kr.mathworks.com/help/matlab/matlab_external/connect-python-to-running-matlab-session.html)




---

## 2. Compiled Python Package


in MATLAB

- Apps -> libraty compiler -> type: python package -> Select `code.m`

> [Calling MATLAB from Python](https://kr.mathworks.com/products/matlab/matlab-and-python.html?fbclid=IwAR3Zd9shiPzSEHlOrtOGzpUY4ssOVz03rFD3dkbjWt944hfX0nKFy6796fs)


in Python 

```python 
import `생성된 패키지 명`

```
