 ```mathetica
 [ CPU request ]
    |
    |
    |
    v
 [ Memory 1 ] --- hit (h1) ---> done in t1
    |
    |
    miss (1-h1)
    |
    v
[ Memory 2 ] --- hit (h2) ---> done in t2 <- but only (1-h1) of requests
    |
    |
    miss (1-h2)
    |
    v
[ Memory 3 ] --- hit (h3) ---> done in t3 <- but onlye (1-h1).(1-h2) of reeusts
```
