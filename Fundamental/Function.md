## 함수 호출

> [함수 한글 설명](https://kr.mathworks.com/help/matlab/referencelist.html?type=function&category=getting-started-with-matlab&s_tid=CRUX_gn_function_getting-started-with-matlab)

- 함수를 변수에 대입하면 함수에서 출력값이 반환됩니다. : `maxA = max(A)`
- 출력 인수가 여러 개인 경우에는 출력 인수를 대괄호로 묶습니다. :`[maxA,location] = max(A)`

- 입력값이 필요 없고 출력값을 반환하지 않는 함수를 호출하려면 함수 이름만 입력하십시오. : `clc` cf. cls()
- 함수 핸들 : 함수를 참조하는 수단으로 사용, 함수 핸들을 작성하려면 함수 이름 앞에 _at_ 기호(`@`)를 사용

- 함수를 파일로 저장시 **파일이름**과 **함수이름**은 같아야 함 

```python 
function r = rank(A,tol)  #함수 이름과 인수의 순서, 두개의 입력, 하나의 출력 
%   RANK Matrix rank.
%   RANK(A) provides an estimate of the number of linearly
%   independent rows or columns of a matrix A.
%   RANK(A,tol) is the number of singular values of A
%   that are larger than tol.
%   RANK(A) uses the default tol = max(size(A)) * norm(A) * eps.

s = svd(A);
if nargin==1
   tol = max(size(A)') * max(s) * eps;
end
r = sum(s > tol);

# 확인 
type rank
```

- [함수 유형 ](https://kr.mathworks.com/help/matlab/learn_matlab/scripts-and-functions.html)
	- 익명 함수 
	- 메인함수 / 로컬 함수 
	- 프라이빗 함수 
	- 중첩 함수 

- 주요 함수 
	- format : 표시되는 값의 수치 형식을 제어 `format short`
	- find : 주어진 논리 조건을 충족하는 배열 요소로 구성된 인덱스를 확인