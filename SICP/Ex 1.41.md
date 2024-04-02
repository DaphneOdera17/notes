```lisp
(define (double f) 
     (lambda (x) (f (f x)))) 
 (( (double (double double) ) inc) 5)
```

$Question: Why~ ~it~ ~outputs~ ~(5 + 16)~ ~instead~ ~of~ ~(5 + 8)~ ~?$
double1 (double2 double3)
double3 -> inc(inc) 2 
double2 double3 -> double3 (double3) 
double1 double -> double3 (double3) (double3 (double3))
相当于 (double3 (double3 (double3 (double3 (inc))))) = 2^4 

inc inc 
inc inc inc inc
inc inc inc inc inc inc inc inc
inc inc inc inc inc inc inc inc inc inc inc inc inc inc inc inc

> if we have n doubles, there will be $2^{2^(n-1)}$ times inc, not $2^n$ times inc.

如果是：
```lisp
(((double (double (double double) ) ) inc) 5)
```
则 (double3 (double3 (double3 (double3 (double3 (double3 (double3 (double3 (inc))))))))) = 2^8

每多一个 double, 要变成 2^{原先}
