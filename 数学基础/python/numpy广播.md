# numpy广播

1. none或np.newaxis

```python
data_s = np.array([[1,1,1],[2,2,2],[3,3,3]])
data_new = np.array([1,2,3])

# if I wanna get data_sub = [[0,0,0], [0,0,0], [0,0,0]]
# 每行减去同一个值
data_sub = data_s - data_new[:, None]

#每行减去同样的数组[1,1,1]
# if you wanna get data_result = 
#[[0,0,0],[1,1,1],[2,2,2]]
data_new1 = np.array([1,1,1])
data_sub2 = data_s - data_new2[None, :]

```

2. 数组复制、扩容

   ```python
   #数组复制：
   a = np.array([0,1,2])
   #1. repeat：
   a2 = a.repreat(2)
   # a2 = ([0,0,1,1,2,2])
   
   #2. tile：
   a3 = a.tile(2)
   # a3 = ([0,1,2,0,1,2])
   ```

   

   