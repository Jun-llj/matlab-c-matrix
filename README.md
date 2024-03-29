# MATLAB与C语言之间的矩阵传递

March 10, 2024 

@jun-llj 

# 发现问题

MATLAB与C语言在矩阵即二维数组方面储存的方式不同，导致矩阵在二者之间的传递会出现问题，矩阵元素被打乱，搜遍全网都没有人发出相关解决代码，所以自己写了一个demo

# 使用方法

1. matlab命令行执行
    
    ```matlab
    mex matrix_demo.c
    ```
    
2. c程序编译成功后，matlab命令行执行
    
    ```matlab
    matrix_demo
    ```
    
3. matlab命令行显示：
    ```matlab
    disp('output_cc在matlab中的输出为:');
    disp(output_cc);
    c在matlab中的输出为:
        0     1     2     3
        4     5     6     7
        8     9    10    11

    matlab的矩阵以一维数组传入c中, 按照c以 行 储存的下标输出为(错误的形式): 
    0.0000004.0000008.0000001.000000
    5.0000009.0000002.0000006.000000
    10.0000003.0000007.00000011.000000

    正确的形式: 
    matlab的矩阵以一维数组传入c中, 按照c以 列 储存的下标输出为(正确的形式): 
    0.0000001.0000002.0000003.000000
    4.0000005.0000006.0000007.000000
    8.0000009.00000010.00000011.000000

    在c中创建指针形式的一维数组c_1d:
    0.0000001.0000002.0000003.000000
    4.0000005.0000006.0000007.000000
    8.0000009.00000010.00000011.000000

    在c中c_1d按照c以 行 储存的下标赋值给二维数组c_2d(正确的形式): 
    c_2d: 
    0.000000 1.000000 2.000000 3.000000 
    4.000000 5.000000 6.000000 7.000000 
    8.000000 9.000000 10.000000 11.000000 

    把从matlab中传来的一维数组形式的矩阵以 列 储存的下标, 赋值给c中创建的二维数组c_2d(正确的形式): 
    c_2d: 
    0.000000 1.000000 2.000000 3.000000 
    4.000000 5.000000 6.000000 7.000000 
    8.000000 9.000000 10.000000 11.000000 

    c中创建的二维数组c_2d赋值给要输出到matlab中的output_cc(正确的形式): 
    output_cc在C中的输出为: 
    0.000000 1.000000 2.000000 3.000000 
    4.000000 5.000000 6.000000 7.000000 
    8.000000 9.000000 10.000000 11.000000 

    output_cc在matlab中的输出为:
        0     1     2     3
        4     5     6     7
        8     9    10    11

    ```
