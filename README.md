# Matlab-fmincon
Matlab求解非线性规划（fmincon函数的使用）
参考链接：

[(25条消息) Matlab求解非线性规划（fmincon函数的使用）_Arcan-CSDN博客_matlab中fmincon](https://blog.csdn.net/Arcann/article/details/109563868?spm=1001.2101.3001.6661.1&utm_medium=distribute.pc_relevant_t0.none-task-blog-2~default~CTRLIST~default-1.highlightwordscore&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-2~default~CTRLIST~default-1.highlightwordscore)

[(25条消息) MATLAB数学建模(3)-非线性规划_超超级钢铁侠-CSDN博客](https://blog.csdn.net/qq_23851075/article/details/51873604?utm_medium=distribute.pc_aggpage_search_result.none-task-blog-2~aggregatepage~first_rank_ecpm_v1~rank_v31_ecpm-1-51873604.pc_agg_new_rank&utm_term=fimincon+matlab&spm=1000.2123.3001.4430)

数据及模型来源：

[基于静力测试数据的桥梁结构有限元模型修正 - 中国知网 (cnki.net)](https://kns.cnki.net/kcms/detail/detail.aspx?dbcode=CMFD&dbname=CMFD2010&filename=2009218955.nh&uniplatform=NZKPT&v=Hb0IQyVTNtMfcqEvWMeRBltys-cmkOOQS9pVdniNpYJsrhJF0JvNHb10_6h8aa-m)

MATLAB中的help文档

>> help fmincon
>> fmincon - Find minimum of constrained nonlinear multivariable function

```matlab
This MATLAB function starts at x0 and attempts to find a minimizer x of the
function described in fun subject to the linear inequalities A*x ≤ b.

x = fmincon(fun,x0,A,b)
x = fmincon(fun,x0,A,b,Aeq,beq)
x = fmincon(fun,x0,A,b,Aeq,beq,lb,ub)
x = fmincon(fun,x0,A,b,Aeq,beq,lb,ub,nonlcon)
x = fmincon(fun,x0,A,b,Aeq,beq,lb,ub,nonlcon,options)
x = fmincon(problem)
[x,fval] = fmincon(___)
[x,fval,exitflag,output] = fmincon(___)
[x,fval,exitflag,output,lambda,grad,hessian] = fmincon(___)

另请参阅 fminbnd, fminsearch, fminunc, optimoptions, optimtool fmincon 的参考页
```

```matlab
options = optimset;
[x, y] = fmincon('fun1', 30*ones(7, 1), [], [], [], [],30*ones(7, 1), 40*ones(7, 1), 'fun2', options)
% 'fun1'代表目标函数，rand(3, 1)随机给了x初值，zeros(3, 1)代表下限为0，即x1, x2, x3>=0, 'fun2'即刚才写的约束条件
————————————————
版权声明：本文为CSDN博主「Arcann」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/Arcann/article/details/109563868
options = optimset;
[x, y] = fmincon('fun1', 30*ones(7, 1), [], [], [], [],30*ones(7, 1), 40*ones(7, 1), 'fun3', options)

```

曾经遇到的错误

>> ```matlab
>> >> f2
>> >> 调用 "fun2" 时，未对输出参数 "h" (可能还包括其他参数)赋值。
>> ```
>
>> 出错 fmincon (line 639)
>>      [ctmp,ceqtmp] = feval(confcn{3},X,varargin{:});
>
>> 出错 f2 (line 2)
>> [x, y] = fmincon('fun1', 30*ones(7, 1), [], [], [], [],30*ones(7, 1), 40*ones(7, 1), 'fun2', options)
>
>> 原因:
>> Failure in initial nonlinear constraint function evaluation. FMINCON cannot continue.
>
>> ```
>> 
>> ```
>
>
>
>> **这是因为约束条件里面有等式约束，所以必须要对等式约束进行说明，没有就是[]，这点很重要**
>
>

目标函数fun1，约束条件fun2，主函数main：

![K6A49{`B_ME3@7P)SI20CFI](https://user-images.githubusercontent.com/73031437/156909169-76e88a5a-6220-4cc9-bd31-b88d814020a6.png)



具体的参数及数据见EXCEL，λ是1，自变量delta p的上下约束为30-40，S为对角矩阵
