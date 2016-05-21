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



###### Largest palindrome product
```clojure
(defn tens
  ([n] (tens n 1))
  ([n x] (if (< n 10) x
                      (tens (quot n 10) (* x 10)))))

(defn reverse'
  [n mult]
  (if (= 0 n) 0
              (+ (* (mod n 10) mult) (reverse' (quot n 10) (quot mult 10)))))

(defn largest-palindrome-product [digits]
(let [max' (reduce * (for [x (range 0 digits)] 10))]
  (apply max (filter #(= (reverse' % (tens %)) %)
                     (for [x (range 1 max') y (range 1 max')] (* x y))))))
```

###### Smallest multiple
```clojure
(defn divdes-all [num s]
  (if (empty? s) true
                 (and (= (mod num (first s)) 0)
                      (divides-all num (rest s)))))

(defn get-divisors
  ([n] (get-divisors (range n 1 -1) []))
  ([s accum]
   (if (empty? s)
     accum
     (let [x (first s)]
       (get-divisors (filter #(not= (mod x %) 0) (rest s)) (conj accum x))))))



(+ 1 (first (filter #(divides-all  (+ 1 %) (get-divisors 20))(range))))
```
