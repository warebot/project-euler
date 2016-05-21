# Project Euler with sprinkles of Clojure
#### Some random Project Euler solutions in Clojure, because, why not.


###### Multiples of 3 and 5
```clojure
(defn sum-multiples-3-5
  [upper-bound]
  (reduce + (filter #(or
                      (= (mod % 5) 0)
                      (= (mod % 3) 0)) (range 1 upper-bound))))


```
###### Even Fibinocci Numbers
```clojure
(defn fib [a b] (lazy-seq (cons a (fib b (+ b a)))))

(reduce + (filter #(= (mod % 2) 0)   (take-while #(< % 4000000) (fib 0 1) )))
```

###### Largest prime factor
```clojure
(defn prime? [x] (not (some #(= (mod x %) 0) (range 2 (+ (Math/sqrt x) 1)))))

(defn prime-factors [x]
  (filter #(and (prime? %) (= (mod x %) 0))
          (range 2 (+ (Math/sqrt x) 1))))

```
