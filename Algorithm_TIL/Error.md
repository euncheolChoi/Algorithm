### 백준 10814
- IndexError :  list assignment index out of range
```
# IndexError : list assignment index out of range가 발생하는 경우
n = int(input())
list = []

for i in range(n):
  list[i] = i
```
- 이런 경우처럼 비어 있는 리스트에 인덱스를 지정했을 때 나오는 에러이다. 이 경우에, 현재 list는 비어 있으므로 NULL값을 가지는데, 인덱스를 지정했으므로 에러가 난다.
**해결 방법 3가지 ** 

- 1) list.append(1)  2) insert(0,1) 3) 리스트에 들어가야 하는 원소의 갯수를 아는경우. 
