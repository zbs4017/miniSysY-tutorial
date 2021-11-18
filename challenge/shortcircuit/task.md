# 挑战实验：短路求值

逻辑与和逻辑或操作符要求总是计算其左操作数，只有在仅靠左操作数的值无法确定该逻辑表达式的结果时，才会求解其右操作数，这被称为短路求值。

在之前的测试样例中，我们并没有针对逻辑表达式的短路求值特性进行评测，**在这个实验中，你需要实现逻辑表达式的短路求值功能**。

在多数情况下，逻辑表达式是否为短路求值并不会对程序的含义产生影响，但是在一些情况下不然。下面给出了一个简单的例子。

```cpp
    int global_variable = 0;  // 全局变量

    int add() {
        global_variable = global_variable + 1;
        return 1;
    }

    int main() {
        if (1 == 1 || 1 == add()) {} // 我们并不想 add() 函数被调用
        return global_variable;
    }
```

若上述代码没有实现逻辑表达式的短路求值特性，则会先判断 `1 == 1`，然后判断 `1 == add()`, 最后将两者的结果进行或操作，这会导致函数 `add()` 的执行，从而导致了全局变量 `global_variable` 的值的改变，这是与我们的期望不符的。

一些更典型且具有实际意义的例子是（当然我们的 miniSysY 语言是没有指针的）

```cpp
// 一个 c 语言中的示例
void * p = NULL;
int ret;
/* ... */
if (p && ret = func(p) ){
}
/* ... */
```

这个例子展示了一种 C 语言中避免对空指针进行存取的方法。

具体指导参考 [短路求值实验指导](help.md)。

## 注意事项

我们会通过调用有副作用的函数的形式来验证你是否完成了短路求值，这意味着我们默认在进行这个实验的时候你已经完成了函数相关的 lab（也就是你的编译器已经支持了函数的定义和函数的调用）。

你需要**认真编写**挑战实验的实验报告，详细说明你是如何完成本次挑战实验的，你对你的编译器进行了哪些改动，你参考了哪些资料，并尽可能完整地阐述你的编译器完成挑战实验任务的工作流程。如果实验报告的内容含糊不清，无法证明你独立完成本次实验，违反 [诚信](../../integrity.md) 原则，我们会酌情扣分。当然，你也需要适当地精简语言，我们对实验报告的评定点在于**扣分**，写出特别长的实验报告（如纯文字内容超过 7 页）并不意味着你能得到加分。

- 实验评测截止时间：2022 年 1 月 2 日 23:59
- 实验报告命名格式：`学号_姓名_shortCircuit.pdf`
- 实验报告提交：[北航云盘](https://bhpan.buaa.edu.cn:443/link/413EA0802B7A7627A6B5112531C40772) `挑战实验/` 对应班级目录中
- 实验报告提交截止时间：2022 年 1 月 2 日 23:59