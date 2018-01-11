---
topic: Verified Code Generation
icon: fa-cogs
pubs:
  - title: "Lazifying case constants"
    id: "afp-lazy-case"
    authors: ["lars"]
    in: "Archive of Formal Proofs, 2017"
    entry: "https://www.isa-afp.org/entries/Lazy_Case.html"
    abstract: |
      Isabelle's code generator performs various adaptations for target languages. Among others, case statements are printed as match expressions. Internally, this is a sophisticated procedure, because in HOL, case statements are represented as nested calls to the case combinators as generated by the datatype package. Furthermore, the procedure relies on laziness of match expressions in the target language, i.e., that branches guarded by patterns that fail to match are not evaluated. Similarly, if-then-else is printed to the corresponding construct in the target language. This entry provides tooling to replace these special cases in the code generator by ignoring these target language features, instead printing case expressions and if-then-else as functions.
  - title: "Constructor Functions"
    id: "afp-constructor-funs"
    authors: ["lars"]
    in: "Archive of Formal Proofs, 2017"
    entry: "https://www.isa-afp.org/entries/Constructor_Funs.html"
    abstract: |
      Isabelle's code generator performs various adaptations for target languages. Among others, constructor applications have to be fully saturated. That means that for constructor calls occuring as arguments to higher-order functions, synthetic lambdas have to be inserted. This entry provides tooling to avoid this construction altogether by introducing constructor functions.
  - title: "Dictionary Construction"
    id: "afp-dict"
    authors: ["lars"]
    in: "Archive of Formal Proofs, 2017"
    entry: "https://www.isa-afp.org/entries/Dict_Construction.html"
    abstract: |
      Isabelle's code generator natively supports type classes. For targets that do not have language support for classes and instances, it performs the well-known dictionary translation, as described by Haftmann and Nipkow. This translation happens outside the logic, i.e., there is no guarantee that it is correct, besides the pen-and-paper proof. This work implements a certified dictionary translation that produces new class-free constants and derives equality theorems.
  - title: "A Verified Compiler from Isabelle/HOL to CakeML"
    id: "isabelle-cakeml"
    authors: ["lars", "tobias"]
    draft: true
    abstract: |
      Many theorem provers can generate functional programs from definitions
      or proofs. However, this code generation needs to be trusted. Except for
      the HOL4 system, which has a proof producing code generator for a subset of ML.
      We go one step further and provide a verified compiler from Isabelle/HOL to CakeML. More precisely we combine a simple proof producing translation of recursion equations in Isabelle/HOL into a deeply embedded term language with a fully verified compilation chain to the target language CakeML.
---

### Goal

Development of a verified code generator from Isabelle/HOL to CakeML, a verified subset of Standard ML.