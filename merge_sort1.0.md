# マージソート

　ソートされた配列を複数（0個以上）受け取って、ソートされた一つの配列を返すアルゴリズム。

　次の関数`merge_arrays(·,·)`はソート済みの二つの配列をつなぎ合わせる（マージする）操作である。

```python
#ソート済みの二つの配列をマージする

def merge_arrays(left, right = []):
	
	res = []
	n, m = len(left), len(right)
	i = 0
	j = 0

	while i < n and j < m:
		if left[i] < right[j]:
			res.append(left[i])
			i += 1
		else:
			res.append(right[j])
			j += 1
	return res + left[i:] + right[j:]
```

　この関数を適用するためには、あらかじめ配列がソートされている必要がある。配列をどんどん分解していくと、最終的に要素が一つの配列が得られる。それらはすでにソートされているとみなせる。

　ある配列を、要素が一つの配列の配列に書き換えるコードが次の`toList(·)`である。

```python
def toList(array):
	return [[v] for v in array]
```

　`toList(·)`で出力された配列を受け取って、要素2の配列からなる配列を作るのが次の`step(·)`である。

```python
#配列の配列を入力とする
def step(array):
  result = []
  for i in range(0,len(array),2):
    result.append(merge_arrays(*array[i:i+2]))
  return result
```

　マージソートは次の構成となっている。

- 配列を配列の配列に変化する
- `step`を、配列の要素数が一つになるまで行う

　上の操作をコードにすると以下の`merge_sort(·)`のようになる。

```python
def merge_sort(array):
	result = toList(array)
  while len(result[0]) != len(array):
    result = step(result)
  return result[0]
```

