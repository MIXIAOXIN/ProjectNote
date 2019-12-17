# numpy中的数组操作：

1. 数组操作，一定要视情况区分数组是深拷贝 还是 共用内存的浅拷贝

   ```python
   #浅拷贝
   a = np.arange(6)
   b = a
   b.reshape((2,3)) #此时，a也会改变形状
   
   #深拷贝
   c = np.array(a, copy=True)
   c.reshape({2,3}) #此时，a.shape依旧为（1，6）
   ```

   

2. ## 数组索引

   1. 

3. ## 数组切片

    

4. ## 数组拼接

   1. #### numpy中$m\times n$的矩阵$a$，现需要变为大小为$m\times （n+1）$的矩阵

      方法一：

      ```python
      c = np.ones(m)
      b = np.c_[a, c] #按列拼接
      
      d = np.ones(n)
      b = np.r_[a, d] #按行拼接
      ```

      方法二：$np.instert()$

      ```python
      c = np.ones(m)
      b = np.inset(a, column_index, values, axis =1) #按列拼接
      b = np.inset(a, 0, valus = c, axis = 1) #拼接c到第0列，最前方
      
      d = np.ones(n)
      b = np.inset(a, row_index, valus, axis = 0] #按行拼接
      ```

      方法三：'column_stack'

      ```python
      np.column_stack((a,c)
      ```





## 



## 



