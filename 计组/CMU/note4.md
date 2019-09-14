# Code Optimization

slides10

## Generally Useful Optimizations

Optimizing Compilers，编译器自动进行的代码优化：
* Code Motion：减少计算的频率，比如把循环内一样的变量计算提出来。
* Reduction in Strength：把开销大的运算改用开销小的方法，比如移位代替乘除法。
* Share Common Subexpressions：把相同的表达写在外部，和Code Motion一样，gcc的`-O1`命令可以实现

## Optimization Blockers

上述编译优化是编译器可能自己执行的，但有些优化编译器无法执行。

### Procedure calls

```c
void lower(char *s) 
{ 
  size_t i; 
  for (i = 0; i < strlen(s); i++) 
    if (s[i] >= 'A' && s[i] <= 'Z') 
      s[i] -= ('A' - 'a'); 
}
```

这里的strlen函数调用，由于是外部函数，编译器认为对这个函数进行移动可能导致错误，因而不会将它移动到循环外部。

### Memory aliasing

```c
/* Sum rows is of n X n matrix a 
and store in vector b */
void sum_rows1(double *a, double *b, long n) {
  long i, j;
  for (i = 0; i < n; i++) {
    b[i] = 0;
    for (j = 0; j < n; j++)
      b[i] += a[i*n + j];
    }
}
```

这里每次访问b[i]时编译器会视为可能影响程序，因此不进行优化。多次访问同一内存位置就叫aliasing。

## Exploiting Instruction-Level Parallelism

采用流水线技术等并行技术，结合硬件结构。Loop Unrolling在每次迭代执行多个操作；Separate Accumulators采用多个并行的运算单元，

## Dealing with Conditionals

分支预测技术，回退等，现在分支预测的成功率很高。