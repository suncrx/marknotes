# Python NumPy 基础入门

掌握数据科学的核心工具

---

## 目录

- NumPy 简介
- 安装与导入
- NumPy 数组的创建
- 数组的基本属性
- 常用数组操作
- 数组的数学运算
- 布尔索引与高级索引
- NumPy 的优势与应用场景
- 总结与实践建议

---

## NumPy 简介

- **定义**：NumPy 是 Python 中用于科学计算的一个基础库，提供了强大的 N 维数组对象和大量用于数组操作的函数。
- **重要性**：在数据科学、机器学习、图像处理等领域广泛应用，是许多其他科学计算库的基础。

---

## 安装与导入

- **安装方法**：
  - 使用 pip 安装：`pip install numpy`
- **导入方式**：
  - `import numpy as np`
- **示例代码**：
  ```python
  import numpy as np
  print(np.__version__)
 
## NumPy 数组的创建

-   **从 Python 列表创建**：
    
    -   `np.array()` 函数
        
    -   示例代码：
        
        PythonCopy
        
        ```python
        my_list = [1, 2, 3, 4]
        np_array = np.array(my_list)
        print(np_array)
        ```
        
-   **使用 NumPy 提供的函数创建**：
    
    -   `np.zeros()`、`np.ones()`、`np.arange()` 等
        
    -   示例代码：
        
        PythonCopy
        
        ```python
        zeros_array = np.zeros((2, 3))
        ones_array = np.ones((3, 2))
        range_array = np.arange(0, 10, 2)
        print(zeros_array)
        print(ones_array)
        print(range_array)
        ```
        

----------

## 数组的基本属性

-   **形状（Shape）**：
    
    -   表示数组的维度大小
        
    -   示例代码：
        
        PythonCopy
        
        ```python
        array = np.array([[1, 2, 3], [4, 5, 6]])
        print(array.shape)
        ```
        
-   **数据类型（dtype）**：
    
    -   指定数组中元素的数据类型
        
    -   示例代码：
        
        PythonCopy
        
        ```python
        array = np.array([1, 2, 3], dtype=np.float32)
        print(array.dtype)
        ```
        
-   **大小（size）**：
    
    -   数组中元素的总数
        
    -   示例代码：
        
        PythonCopy
        
        ```python
        array = np.array([[1, 2, 3], [4, 5, 6]])
        print(array.size)
        ```
        
-   **维度（ndim）**：
    
    -   数组的维度数
        
    -   示例代码：
        
        PythonCopy
        
        ```python
        array = np.array([[1, 2, 3], [4, 5, 6]])
        print(array.ndim)
        ```
        

----------

## 常用数组操作

-   **数组的切片与索引**：
    
    -   一维数组的切片
        
    -   多维数组的切片
        
    -   示例代码：
        
        PythonCopy
        
        ```python
        array = np.array([0, 1, 2, 3, 4, 5])
        print(array[1:4])
        multi_array = np.array([[1, 2, 3], [4, 5, 6]])
        print(multi_array[0, 1])
        print(multi_array[1, :])
        ```
        
-   **数组的重塑（reshape）**：
    
    -   改变数组的形状而不改变其数据
        
    -   示例代码：
        
        PythonCopy
        
        ```python
        array = np.arange(6)
        reshaped_array = array.reshape((2, 3))
        print(reshaped_array)
        ```
        
-   **数组的合并与分割**：
    
    -   `np.concatenate()`、`np.split()` 等
        
    -   示例代码：
        
        PythonCopy
        
        ```python
        array1 = np.array([1, 2, 3])
        array2 = np.array([4, 5, 6])
        concatenated_array = np.concatenate((array1, array2))
        print(concatenated_array)
        ```
        

----------

## 数组的数学运算

-   **逐元素运算**：
    
    -   加、减、乘、除等
        
    -   示例代码：
        
        PythonCopy
        
        ```python
        array1 = np.array([1, 2, 3])
        array2 = np.array([4, 5, 6])
        print(array1 + array2)
        print(array1 * array2)
        ```
        
-   **聚合运算**：
    
    -   求和（`np.sum()`）、平均值（`np.mean()`）、最大值（`np.max()`）等
        
    -   示例代码：
        
        PythonCopy
        
        ```python
        array = np.array([1, 2, 3, 4, 5])
        print(np.sum(array))
        print(np.mean(array))
        print(np.max(array))
        ```
        
-   **广播机制**：
    
    -   简单介绍广播规则
        
    -   示例代码：
        
        PythonCopy
        
        ```python
        array = np.array([[1, 2, 3], [4, 5, 6]])
        scalar = 2
        print(array * scalar)
        ```
        

----------

## 布尔索引与高级索引

-   **布尔索引**：
    
    -   根据条件筛选数组元素
        
    -   示例代码：
        
        PythonCopy
        
        ```python
        array = np.array([1, 2, 3, 4, 5])
        condition = array > 3
        print(array[condition])
        ```
        
-   **高级索引**：
    
    -   使用整数数组进行索引
        
    -   示例代码：
        
        PythonCopy
        
        ```python
        array = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
        row_indices = [0, 2]
        col_indices = [1, 2]
        print(array[row_indices, col_indices])
        ```
        

----------

## NumPy 的优势与应用场景

-   **优势**：
    
    -   高效的数组操作
        
    -   内置大量数学函数
        
    -   广泛的社区支持
        
-   **应用场景**：
    
    -   数据分析与处理
        
    -   机器学习与人工智能
        
    -   图像处理与计算机视觉
        
    -   科学计算与工程应用
        

----------

## 总结与实践建议

-   **总结**：回顾 NumPy 的基本概念、数组操作、数学运算等内容。
    
-   **实践建议**：
    
    -   多练习，熟悉 NumPy 的常用函数和操作。
        
    -   阅读官方文档，了解更高级的功能。
        
    -   结合实际项目，应用 NumPy 解决实际问题。
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTgwNzY3MTM4Ml19
-->