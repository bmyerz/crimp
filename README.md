crimp
=====

Certified Relational to Imperative.

The goal of this project is a verified compiler from SQL-like
queries to imperative code.

The core theorem statement is of a similar form to other translation equivalence theorems.
```coq
Theorem queryEquivalence:
  forall (q : Query) (p : ImpProgram),
    queryToImp q = Some p ->
      forall (r1 r2 r' : relation), runQuery q r1 r2 = Some r' ->
        runImp' p r1 r2 = Some r'.
```
Or 

_if the compiler accepts the query, and the query produces successful output according to the semantics of relational algebra(+), then the Imp program will
succeed and produce the same output_

Inspired by verifying transformations in [Raco](https://github.com/uwescience/raco).

### Dependencies
- Coq 8.4+ (tested at 8.4, may work with down to 8.2)
- [Tactics from Certified Programming with Dependent Types](http://adam.chlipala.net/cpdt/cpdtlib.tgz)

### Get Coq dependencies
```bash
wget http://adam.chlipala.net/cpdt/cpdtlib.tgz
tar xf cpdtlib.tgz
cd cpdtlib
coqc CpdtTactics
```

### Build Crimp
```bash
export CPDT_HOME=/path/to/cpdtlib
cd crimp
make
```

### Run Crimp proofs
You can run the query equivalence proofs with
```bash
make QueryEquivalence.vo
```

or you can open QueryEquivalence.v in your favorite/un-favorite Coq environment, like [Proof General](http://proofgeneral.inf.ed.ac.uk).
