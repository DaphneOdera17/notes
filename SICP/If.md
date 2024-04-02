

自定义一个 $if$

```lisp
(define (iff <p> <c> <a>) (if <p> <c> <a>)) 
(define (tryif a) (if (= a 0) 1 (/ 1 0))) 
(define (tryiff a) (iff (= a 0) 1 (/ 1 0))) 
```

```lisp
>(tryif 0)
1
>(tryif 1)
../:division by zero
> (tryiff 0)
. . /: division by zero
> (tryiff 1)
. . /: division by zero
```

默认的 $if$ 语句是一种特殊形式，这意味着即使解释器遵循应用替换，它也只计算其中一个参数，而不是同时计算两个参数。

而这里的 $tryiff$ 就会进行 $(1 / 0)$