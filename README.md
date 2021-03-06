hindley_milner
==============

An implementation of the Hindley-Milner type checking algorithm based on the [Python code by Robert Smallshire](http://www.smallshire.org.uk/sufficientlysmall/2010/04/11/a-hindley-milner-type-inference-implementation-in-python/), the [Scala code by Andrew Forrest](http://dysphoria.net/2009/06/28/hindley-milner-type-inference-in-scala/), the Perl code by Nikita Borisov, and [the paper "Basic Polymorphic Typechecking" by Cardelli](http://lucacardelli.name/Papers/BasicTypechecking.pdf).

Interestingly, this implementation makes extensive use of ```boost::variant``` and ```boost::apply_visitor```.

Build the demo program with:

```
$ scons
```

Run the demo program with:

```
$ ./demo
(letrec factorial = (fn n => (((cond (zero n)) 1) ((times n) (factorial (pred n))))) in (factorial 5)) : int
(fn x => ((pair (x 3)) (x true))) : type mismatch: bool != int
((pair (f 4)) (f true)) : Undefined symbol f
(let f = (fn x => x) in ((pair (f 4)) (f true))) : (int * bool)
(fn f => (f f)) : recursive unification: a in (a -> b)
(let g = (fn f => 5) in (g g)) : int
(fn g => (let f = (fn x => g) in ((pair (f 3)) (f true)))) : (a -> (a * a))
(fn f => (fn g => (fn arg => (g (f arg))))) : ((a -> b) -> ((b -> c) -> (a -> c)))
(fn f => (f 5)) : ((int -> a) -> a)
((fn y => (y 1)) (fn x => 1)) : int
```
