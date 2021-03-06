---
topic: Verified Code Generation
icon: fa-cogs
pubs:
  - title: "Lazifying case constants"
    id: "afp-lazy-case"
    authors: ["lars"]
    in: "Archive of Formal Proofs"
    year: 2017
    entry: "https://www.isa-afp.org/entries/Lazy_Case.html"
    abstract: |
      Isabelle's code generator performs various adaptations for target languages. Among others, case statements are printed as match expressions. Internally, this is a sophisticated procedure, because in HOL, case statements are represented as nested calls to the case combinators as generated by the datatype package. Furthermore, the procedure relies on laziness of match expressions in the target language, i.e., that branches guarded by patterns that fail to match are not evaluated. Similarly, if-then-else is printed to the corresponding construct in the target language. This entry provides tooling to replace these special cases in the code generator by ignoring these target language features, instead printing case expressions and if-then-else as functions.
  - title: "Constructor Functions"
    id: "afp-constructor-funs"
    authors: ["lars"]
    in: "Archive of Formal Proofs"
    year: 2017
    entry: "https://www.isa-afp.org/entries/Constructor_Funs.html"
    abstract: |
      Isabelle's code generator performs various adaptations for target languages. Among others, constructor applications have to be fully saturated. That means that for constructor calls occuring as arguments to higher-order functions, synthetic lambdas have to be inserted. This entry provides tooling to avoid this construction altogether by introducing constructor functions.
  - title: "Dictionary Construction"
    id: "afp-dict"
    authors: ["lars"]
    in: "Archive of Formal Proofs"
    year: 2017
    entry: "https://www.isa-afp.org/entries/Dict_Construction.html"
    abstract: |
      Isabelle's code generator natively supports type classes. For targets that do not have language support for classes and instances, it performs the well-known dictionary translation, as described by Haftmann and Nipkow. This translation happens outside the logic, i.e., there is no guarantee that it is correct, besides the pen-and-paper proof. This work implements a certified dictionary translation that produces new class-free constants and derives equality theorems.
  - title: "A Verified Compiler from Isabelle/HOL to CakeML"
    id: "isabelle-cakeml"
    authors: ["lars", "tobias"]
    in: "European Symposium on Programming (ESOP, Open Access)"
    errata: true
    springer: true
    year: 2018
    doi: "10.1007/978-3-319-89884-1_35"
    select: true
    abstract: |
      Many theorem provers can generate functional programs from definitions
      or proofs. However, this code generation needs to be trusted. Except for
      the HOL4 system, which has a proof producing code generator for a subset of ML.
      We go one step further and provide a verified compiler from Isabelle/HOL to CakeML. More precisely we combine a simple proof producing translation of recursion equations in Isabelle/HOL into a deeply embedded term language with a fully verified compilation chain to the target language CakeML.
  - title: "Isabelle/CakeML"
    id: "afp-cakeml"
    authors: ["lars", "yu"]
    entry: "https://www.isa-afp.org/entries/CakeML.html"
    year: 2018
    abstract: |
      CakeML is a functional programming language with a proven-correct compiler and runtime system. This entry contains an unofficial version of the CakeML semantics that has been exported from the Lem specifications to Isabelle. Additionally, there are some hand-written theory files that adapt the exported code to Isabelle and port proofs from the HOL4 formalization, e.g. termination and equivalence proofs.
  - title: "Certifying Dictionary Construction in Isabelle/HOL"
    id: "dict"
    authors: ["lars"]
    draft: yes
    year: 2018
    abstract: |
      Type classes are a well-known extensions to various type systems. Classes usually participate in type inference; that is, the type checker will automatically deduce class constraints and select appropriate instances. Compilers for such languages face the challenge that concrete instances are generally not directly mentioned in the source text. In the runtime, type class operations need to be packaged into dictionaries that are passed around as pointers. This article presents the most common approach for compilation of type classes – the dictionary construction – carried out in a trustworthy fashion in Isabelle/HOL, a proof assistant.
  - title: "An Algebra for Higher-Order Terms"
    id: "afp-terms"
    authors: ["lars"]
    entry: "https://www.isa-afp.org/entries/Higher_Order_Terms.html"
    year: 2019
    abstract: |
      In this formalization, I introduce a higher-order term algebra, generalizing the notions of free variables, matching, and substitution. The need arose from the work on a verified compiler from Isabelle to CakeML. Terms can be thought of as consisting of a generic (free variables, constants, application) and a specific part. As example applications, this entry provides instantiations for de-Bruijn terms, terms with named variables, and Blanchette’s λ-free higher-order terms. Furthermore, I implement translation functions between de-Bruijn terms and named terms and prove their correctness.
  - title: "Verified Code Generation from Isabelle/HOL"
    id: "phd-thesis_hupel"
    authors: ["lars"]
    bib: false
    year: 2019
    abstract: |
      In this thesis, I develop a verified compilation toolchain from executable specifications in Isabelle/HOL to CakeML abstract syntax trees.
      This improves over the state-of-the-art in Isabelle by providing a trustworthy procedure for code generation.
      The work consists of three major contributions.
      <br />
      First, I have implemented a certifying routine to eliminate type classes and instances in Isabelle specifications.
      Based on defining equations of constants, it derives new definitions that do not use type classes.
      This can be used to bypass an unverified step in the current code generator.
      <br />
      Second, I formalized an algebra for higher-order λ-terms that generalizes the notions of free variables, matching, and substitution.
      Terms can be thought of as consisting of a generic (free variables, constants, application) and a specific part (abstraction, bound variables).
      With this algebra, it becomes possible to reason abstractly over a variety of different types.
      <br />
      These two parts are independent from each other and can also be used for other purposes.
      For example, I have successfully instantiated the term algebra for other term types in the Isabelle universe.
      <br />
      Third, a compiler that works similarly to the existing code generator, but produces a CakeML abstract syntax tree together with a correctness theorem.
      More precisely, I have combined a simple proof producing translation of recursion equations in Isabelle into a deeply embedded term language with a fully verified compilation chain to the target language CakeML.

---

### Goal

Development of a verified code generator from Isabelle/HOL to CakeML, a verified subset of Standard ML.
The vision of this project is to provide an alternative (or extension) to the current code generation facility that reduces the trusted code base.

### FAQ

What is the trusted code base of the pipeline?
: We rely on faithful export from Lem to Isabelle, an unverified printer of CakeML AST to CakeML source text, and the kernel of Isabelle.
There is ongoing work to use [OpenTheory](http://www.gilith.com/software/opentheory/) to get a more faithful representation of the CakeML formalization in Isabelle.

Does the pipeline target existing CakeML library constructs, like the built-in lists?
: No, it does not, and it is not intended at the moment.

Does the pipeline target existing CakeML native constructs, like machine integers?
: No, it does not, but it is intended for the future, and actively being worked on.

Does that mean that arithmetic on natural numbers in Isabelle is mapped to unary in CakeML?
: That is accurate: `nat`s are treated as a proper datatype with `Zero` and `Suc` constructors.

How are (8-bit) characters treated?
: The most naive possible translation, 256-way enumerations, would lead to very large code sizes. Instead, we translate characters to bytes, i.e. 8-tuples of `bool`s.
[As of Isabelle2018](http://isabelle.in.tum.de/repos/isabelle/rev/1f9f973eed2a), this will become the default of code generation in Isabelle, including other (unverified) targets.

Is the generated code guaranteed to terminate?
: The current Isabelle code generator only guarantees partial correctness (which has been proved on paper).
While our work is designed for total correctness (all functions that are exported are internally proved to be terminating), we have only proved partial correctness so far.
The CakeML compiler team has proved total correctness.<br>
_Update, August 2018:_ Some (not all) compiler phases have been proved to be totally correct.

Why isn't there a full compilation pipeline in the AFP?
: We're working on it.
Some parts of it are already available as stand-alone entries, and we want to make sure it's published in modular parts.
In the meantime, use the packaged version that accompanies the main paper ([see below](#supplementary-material)).

### Supplementary Material

* [Formalization for "A Verified Compiler from Isabelle/HOL to CakeML"](/pub/isabelle-cakeml-supplements.zip)<br>
  Submitted: 2017-10-20<br>
  Archived as: DOI [10.5281/zenodo.1167616](http://doi.org/10.5281/zenodo.1167616)

### Errata

The ESOP'18 paper has an error in Definition 7 (page 20), third rule (`Vrecabs`), second line.
After the bounded quantifiers (before the ≈ operator), instead of σ₁, it should read _rs_.
This is an error in the transcription from the formalization (supplementary material) to the paper.
The error is not present in the supplementary material.
Explanation:
The second precondition of the `Vrecabs` case should compare the constants with the rule set _rs_.
σ₁ is the variable environment from the previous semantics and does not carry constant definitions.
