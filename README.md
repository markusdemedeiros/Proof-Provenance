# The Proof Provenance System

Formal verification can serve a variety of purposes, and engaging with the verification community means clearly communicating what that purpose is. The Proof Provenance System is a shorthand for describing how you want people to engage with your formally verified piece of software.

Below are five classes a formalization project might fit into.
The system is not a rubric! 
While lower down classes are generally considered higher quality, they much more stringent and much less agile, which is not appropriate for all verification tasks. 

Think about this system less as a measure of quality and more as a protocol for how you expect others to engage with your project. 
An accurate classification tells the world of potential collaborators what they can depend on *you* for, and dually, lays down some guidelines you'd expect new collaborators to respect.

## Bare formalization [![Proof Provenance][fc-class-bare]][fc-link]
- I make **no assertions** about the code

Bare formalizations are rare, free, and they abdicate any responsibility about the work itself. Nevertheless, marking a formalization as bare is still helpful to readers, as a kind of "opt-out". 

## Certificate formalization [![Proof Provenance][fc-class-certificate]][fc-link]
- The project establishes **truth** of some formal statement, which may only be loosely understood.
- I vouch that the project compiles.

A certificate formalization is useful when mere truth itself is the only goal. This provides evidence that a formalization of some result is possible.

#### Examples
- A proof translated into Lean out of a Vampire run.
- A proof generated autonomously by an LLM.
- A corpus of possible "junk theorems", which may or may not be intelligible, but can still be used to close proof goals. 
 
## Prototype formalization [![Proof Provenance][fc-class-prototype]][fc-link]
- The project establishes a baseline formalization of a **clearly-scoped** result.
- I vouch that the project does not make use of exploits or **trivializing loopholes**. 
- I (human) can vouch that the formalizations of the main statements are a faithful formal representation of commonly held definitions.

A prototype formalization is useful to establish a high-level verification methodology which future work can refine and extract knowledge from.

#### Examples
- A proof with some autonomously generated components but with human-crafted theorem statements.
- Autoformalizations of results that are easily stated using existing Mathlib machinery, such as numerical bounds. 

## Reference formalization [![Proof Provenance][fc-class-reference]][fc-link]
- The project establishes **curated** and **reusable** proof techniques for a **clearly-scoped** result.
- I (human) am capable of explaining why the code is formalized the way it is.
- The project is stable. Pinned versions of the project will be hosted indefinitely and can be used as a dependency.

Reference formalizations signal that a piece of code is reusable, stable, and functionally complete. Dependents of reference formalizations should expect that they would be able to use the code without modifying it.

#### Examples
- Actively curated software libraries.
- Proof artifacts associated to published papers ("Artifacts Evaluated -- Reusable", in ACM parlance).

## Canonical formalization [![Proof Provenance][fc-class-canonical]][fc-link]
- The project is **decisively scoped** and should be considered the **definitive** formalization.
- I (human) am an expert in all of the code present. 
- I (human) commit to the upkeep and curation of the project for the foreseeable future, including responding to feature and pull requests.
- I commit to coordinating with other canonical formalizations to ensure mutual compatibility.
- I will allow my project to be absorbed into another canonical formalization, so that only one definitive version exists.

Canonical formalizations are rare. Mathlib is one such example.

# A note on `sorry`, and otherwise open proofs
As the quality and investment into a project increases, so does the ability for experts to make informed decisions about open proofs. This runs contrary to the idea that "sorry-free" is a measure of a formalization's quality. Some examples: 

- In the absence of a deep understanding of the proofs at hand, a `sorry` can seriously undermine the mere truth of a formal statement in unpredictable. Certificate proofs likely should be sorry-free.
- A well-communuicated `sorry` may be acceptable in some prototype proofs. For example, an expert maintainer may judge a `sorry` may be acceptable when a proof is pending an upstream definition, provided they are confident that any such definition will do.
- Canonical or reference formalizations may choose to permanently include axioms depending on their application domain (for example, `native_decide` for program verification). However, one would expect a canonical formalization to be extremely conservative in this regard, in order to preserve compatibility with projects that have stricter requirements. 

# More Info

This system builds on Terence Tao's "Techniques and Tools for the Formalization of Analysis" workshop talk,[^1] where Tao takes a first cut at broadly classifying different standards for formalized mathematics.
I wanted to expand on this system a little, and tweak it to be suitable for software verification as well.

The classification is, of course, opt-in and can only be socially enforced.
To that end, it intentionally makes no moral claims about the usage of any technology such as large language models.
Rather, the perspective here is intended to be much more positive, and focus on the immense value of human expertise in collaborative verification projects.
I believe that better communication to this end can help us all get on the same page and work on bigger projects, together.


# GitHub Badges
To add a badge to your repository,
1. Copy the following code block to the bottom of your `README.md`
```
[fc-link]: https://github.com/markusdemedeiros/Proof-Provenance
[fc-class-bare]: https://img.shields.io/badge/proof%20provenance-bare-black?logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCA1MTIgNTEyIiBmaWxsPSJ3aGl0ZSI+PHBhdGggZD0iTTE3NiAyNGMwLTEzLjMtMTAuNy0yNC0yNC0yNHMtMjQgMTAuNy0yNCAyNFY2NGMtMzUuMyAwLTY0IDI4LjctNjQgNjRIMjRjLTEzLjMgMC0yNCAxMC43LTI0IDI0czEwLjcgMjQgMjQgMjRINjR2NTZIMjRjLTEzLjMgMC0yNCAxMC43LTI0IDI0czEwLjcgMjQgMjQgMjRINjR2NTZIMjRjLTEzLjMgMC0yNCAxMC43LTI0IDI0czEwLjcgMjQgMjQgMjRINjRjMCAzNS4zIDI4LjcgNjQgNjQgNjR2NDBjMCAxMy4zIDEwLjcgMjQgMjQgMjRzMjQtMTAuNyAyNC0yNFY0NDhoNTZ2NDBjMCAxMy4zIDEwLjcgMjQgMjQgMjRzMjQtMTAuNyAyNC0yNFY0NDhoNTZ2NDBjMCAxMy4zIDEwLjcgMjQgMjQgMjRzMjQtMTAuNyAyNC0yNFY0NDhjMzUuMyAwIDY0LTI4LjcgNjQtNjRoNDBjMTMuMyAwIDI0LTEwLjcgMjQtMjRzLTEwLjctMjQtMjQtMjRINDQ4VjI4MGg0MGMxMy4zIDAgMjQtMTAuNyAyNC0yNHMtMTAuNy0yNC0yNC0yNEg0NDhWMTc2aDQwYzEzLjMgMCAyNC0xMC43IDI0LTI0cy0xMC43LTI0LTI0LTI0SDQ0OGMwLTM1LjMtMjguNy02NC02NC02NFYyNGMwLTEzLjMtMTAuNy0yNC0yNC0yNHMtMjQgMTAuNy0yNCAyNFY2NEgyODBWMjRjMC0xMy4zLTEwLjctMjQtMjQtMjRzLTI0IDEwLjctMjQgMjRWNjRIMTc2VjI0ek0xNjAgMTI4SDM1MmMxNy43IDAgMzIgMTQuMyAzMiAzMlYzNTJjMCAxNy43LTE0LjMgMzItMzIgMzJIMTYwYy0xNy43IDAtMzItMTQuMy0zMi0zMlYxNjBjMC0xNy43IDE0LjMtMzIgMzItMzJ6bTE5MiAzMkgxNjBWMzUySDM1MlYxNjB6Ii8+PC9zdmc+Cg==
[fc-class-certificate]: https://img.shields.io/badge/proof%20provenance-certificate-black?logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCA1MTIgNTEyIiBmaWxsPSJ3aGl0ZSI+PHBhdGggZD0iTTMxMiAyMDEuOGMwLTE3LjQgOS4yLTMzLjIgMTkuOS00N0MzNDQuNSAxMzguNSAzNTIgMTE4LjEgMzUyIDk2YzAtNTMtNDMtOTYtOTYtOTZzLTk2IDQzLTk2IDk2YzAgMjIuMSA3LjUgNDIuNSAyMC4xIDU4LjhjMTAuNyAxMy44IDE5LjkgMjkuNiAxOS45IDQ3YzAgMjkuOS0yNC4zIDU0LjItNTQuMiA1NC4yTDExMiAyNTZDNTAuMSAyNTYgMCAzMDYuMSAwIDM2OGMwIDIwLjkgMTMuNCAzOC43IDMyIDQ1LjNMMzIgNDY0YzAgMjYuNSAyMS41IDQ4IDQ4IDQ4bDM1MiAwYzI2LjUgMCA0OC0yMS41IDQ4LTQ4bDAtNTAuN2MxOC42LTYuNiAzMi0yNC40IDMyLTQ1LjNjMC02MS45LTUwLjEtMTEyLTExMi0xMTJsLTMzLjggMGMtMjkuOSAwLTU0LjItMjQuMy01NC4yLTU0LjJ6TTQxNiA0MTZsMCAzMkw5NiA0NDhsMC0zMiAzMjAgMHoiLz48L3N2Zz4K
[fc-class-prototype]: https://img.shields.io/badge/proof%20provenance-prototype-black?logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCA0NDggNTEyIiBmaWxsPSJ3aGl0ZSI+PHBhdGggZD0iTTI4OCAwTDE2MCAwIDEyOCAwQzExMC4zIDAgOTYgMTQuMyA5NiAzMnMxNC4zIDMyIDMyIDMybDAgMTMyLjhjMCAxMS44LTMuMyAyMy41LTkuNSAzMy41TDEwLjMgNDA2LjJDMy42IDQxNy4yIDAgNDI5LjcgMCA0NDIuNkMwIDQ4MC45IDMxLjEgNTEyIDY5LjQgNTEybDMwOS4yIDBjMzguMyAwIDY5LjQtMzEuMSA2OS40LTY5LjRjMC0xMi44LTMuNi0yNS40LTEwLjMtMzYuNEwzMjkuNSAyMzAuNGMtNi4yLTEwLjEtOS41LTIxLjctOS41LTMzLjVMMzIwIDY0YzE3LjcgMCAzMi0xNC4zIDMyLTMycy0xNC4zLTMyLTMyLTMyTDI4OCAwek0xOTIgMTk2LjhMMTkyIDY0bDY0IDAgMCAxMzIuOGMwIDIzLjcgNi42IDQ2LjkgMTkgNjcuMUwzMDkuNSAzMjBsLTE3MSAwTDE3MyAyNjMuOWMxMi40LTIwLjIgMTktNDMuNCAxOS02Ny4xeiIvPjwvc3ZnPgo=
[fc-class-reference]: https://img.shields.io/badge/proof%20provenance-reference-black?logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCA0NDggNTEyIiBmaWxsPSJ3aGl0ZSI+PHBhdGggZD0iTTk2IDBDNDMgMCAwIDQzIDAgOTZMMCA0MTZjMCA1MyA0MyA5NiA5NiA5NmwyODggMCAzMiAwYzE3LjcgMCAzMi0xNC4zIDMyLTMycy0xNC4zLTMyLTMyLTMybDAtNjRjMTcuNyAwIDMyLTE0LjMgMzItMzJsMC0zMjBjMC0xNy43LTE0LjMtMzItMzItMzJMMzg0IDAgOTYgMHptMCAzODRsMjU2IDAgMCA2NEw5NiA0NDhjLTE3LjcgMC0zMi0xNC4zLTMyLTMyczE0LjMtMzIgMzItMzJ6bTMyLTI0MGMwLTguOCA3LjItMTYgMTYtMTZsMTkyIDBjOC44IDAgMTYgNy4yIDE2IDE2cy03LjIgMTYtMTYgMTZsLTE5MiAwYy04LjggMC0xNi03LjItMTYtMTZ6bTE2IDQ4bDE5MiAwYzguOCAwIDE2IDcuMiAxNiAxNnMtNy4yIDE2LTE2IDE2bC0xOTIgMGMtOC44IDAtMTYtNy4yLTE2LTE2czcuMi0xNiAxNi0xNnoiLz48L3N2Zz4K
[fc-class-canonical]: https://img.shields.io/badge/proof%20provenance-canonical-black?logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCA1MTIgNTEyIiBmaWxsPSJ3aGl0ZSI+PHBhdGggZD0iTTI0My40IDIuNmwtMjI0IDk2Yy0xNCA2LTIxLjggMjEtMTguNyAzNS44UzE2LjggMTYwIDMyIDE2MGwwIDhjMCAxMy4zIDEwLjcgMjQgMjQgMjRsNDAwIDBjMTMuMyAwIDI0LTEwLjcgMjQtMjRsMC04YzE1LjIgMCAyOC4zLTEwLjcgMzEuMy0yNS42cy00LjgtMjkuOS0xOC43LTM1LjhsLTIyNC05NmMtOC0zLjQtMTcuMi0zLjQtMjUuMiAwek0xMjggMjI0bC02NCAwIDAgMTk2LjNjLS42IC4zLTEuMiAuNy0xLjggMS4xbC00OCAzMmMtMTEuNyA3LjgtMTcgMjIuNC0xMi45IDM1LjlTMTcuOSA1MTIgMzIgNTEybDQ0OCAwYzE0LjEgMCAyNi41LTkuMiAzMC42LTIyLjdzLTEuMS0yOC4xLTEyLjktMzUuOWwtNDgtMzJjLS42LS40LTEuMi0uNy0xLjgtMS4xTDQ0OCAyMjRsLTY0IDAgMCAxOTItNDAgMCAwLTE5Mi02NCAwIDAgMTkyLTQ4IDAgMC0xOTItNjQgMCAwIDE5Mi00MCAwIDAtMTkyek0yNTYgNjRhMzIgMzIgMCAxIDEgMCA2NCAzMiAzMiAwIDEgMSAwLTY0eiIvPjwvc3ZnPgo=
```
2. Add the appropriate badge to the top, for example ``[![Proof Provenance][fc-class-reference]][fc-link]``

[^1]: [video](https://icerm.brown.edu/video_archive/4649). Tao's system is presented at around the 25 minute mark. 

[fc-link]: https://github.com/markusdemedeiros/Proof-Provenance
[fc-class-bare]: https://img.shields.io/badge/proof%20provenance-bare-black?logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCA1MTIgNTEyIiBmaWxsPSJ3aGl0ZSI+PHBhdGggZD0iTTE3NiAyNGMwLTEzLjMtMTAuNy0yNC0yNC0yNHMtMjQgMTAuNy0yNCAyNFY2NGMtMzUuMyAwLTY0IDI4LjctNjQgNjRIMjRjLTEzLjMgMC0yNCAxMC43LTI0IDI0czEwLjcgMjQgMjQgMjRINjR2NTZIMjRjLTEzLjMgMC0yNCAxMC43LTI0IDI0czEwLjcgMjQgMjQgMjRINjR2NTZIMjRjLTEzLjMgMC0yNCAxMC43LTI0IDI0czEwLjcgMjQgMjQgMjRINjRjMCAzNS4zIDI4LjcgNjQgNjQgNjR2NDBjMCAxMy4zIDEwLjcgMjQgMjQgMjRzMjQtMTAuNyAyNC0yNFY0NDhoNTZ2NDBjMCAxMy4zIDEwLjcgMjQgMjQgMjRzMjQtMTAuNyAyNC0yNFY0NDhoNTZ2NDBjMCAxMy4zIDEwLjcgMjQgMjQgMjRzMjQtMTAuNyAyNC0yNFY0NDhjMzUuMyAwIDY0LTI4LjcgNjQtNjRoNDBjMTMuMyAwIDI0LTEwLjcgMjQtMjRzLTEwLjctMjQtMjQtMjRINDQ4VjI4MGg0MGMxMy4zIDAgMjQtMTAuNyAyNC0yNHMtMTAuNy0yNC0yNC0yNEg0NDhWMTc2aDQwYzEzLjMgMCAyNC0xMC43IDI0LTI0cy0xMC43LTI0LTI0LTI0SDQ0OGMwLTM1LjMtMjguNy02NC02NC02NFYyNGMwLTEzLjMtMTAuNy0yNC0yNC0yNHMtMjQgMTAuNy0yNCAyNFY2NEgyODBWMjRjMC0xMy4zLTEwLjctMjQtMjQtMjRzLTI0IDEwLjctMjQgMjRWNjRIMTc2VjI0ek0xNjAgMTI4SDM1MmMxNy43IDAgMzIgMTQuMyAzMiAzMlYzNTJjMCAxNy43LTE0LjMgMzItMzIgMzJIMTYwYy0xNy43IDAtMzItMTQuMy0zMi0zMlYxNjBjMC0xNy43IDE0LjMtMzIgMzItMzJ6bTE5MiAzMkgxNjBWMzUySDM1MlYxNjB6Ii8+PC9zdmc+Cg==
[fc-class-certificate]: https://img.shields.io/badge/proof%20provenance-certificate-black?logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCA1MTIgNTEyIiBmaWxsPSJ3aGl0ZSI+PHBhdGggZD0iTTMxMiAyMDEuOGMwLTE3LjQgOS4yLTMzLjIgMTkuOS00N0MzNDQuNSAxMzguNSAzNTIgMTE4LjEgMzUyIDk2YzAtNTMtNDMtOTYtOTYtOTZzLTk2IDQzLTk2IDk2YzAgMjIuMSA3LjUgNDIuNSAyMC4xIDU4LjhjMTAuNyAxMy44IDE5LjkgMjkuNiAxOS45IDQ3YzAgMjkuOS0yNC4zIDU0LjItNTQuMiA1NC4yTDExMiAyNTZDNTAuMSAyNTYgMCAzMDYuMSAwIDM2OGMwIDIwLjkgMTMuNCAzOC43IDMyIDQ1LjNMMzIgNDY0YzAgMjYuNSAyMS41IDQ4IDQ4IDQ4bDM1MiAwYzI2LjUgMCA0OC0yMS41IDQ4LTQ4bDAtNTAuN2MxOC42LTYuNiAzMi0yNC40IDMyLTQ1LjNjMC02MS45LTUwLjEtMTEyLTExMi0xMTJsLTMzLjggMGMtMjkuOSAwLTU0LjItMjQuMy01NC4yLTU0LjJ6TTQxNiA0MTZsMCAzMkw5NiA0NDhsMC0zMiAzMjAgMHoiLz48L3N2Zz4K
[fc-class-prototype]: https://img.shields.io/badge/proof%20provenance-prototype-black?logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCA0NDggNTEyIiBmaWxsPSJ3aGl0ZSI+PHBhdGggZD0iTTI4OCAwTDE2MCAwIDEyOCAwQzExMC4zIDAgOTYgMTQuMyA5NiAzMnMxNC4zIDMyIDMyIDMybDAgMTMyLjhjMCAxMS44LTMuMyAyMy41LTkuNSAzMy41TDEwLjMgNDA2LjJDMy42IDQxNy4yIDAgNDI5LjcgMCA0NDIuNkMwIDQ4MC45IDMxLjEgNTEyIDY5LjQgNTEybDMwOS4yIDBjMzguMyAwIDY5LjQtMzEuMSA2OS40LTY5LjRjMC0xMi44LTMuNi0yNS40LTEwLjMtMzYuNEwzMjkuNSAyMzAuNGMtNi4yLTEwLjEtOS41LTIxLjctOS41LTMzLjVMMzIwIDY0YzE3LjcgMCAzMi0xNC4zIDMyLTMycy0xNC4zLTMyLTMyLTMyTDI4OCAwek0xOTIgMTk2LjhMMTkyIDY0bDY0IDAgMCAxMzIuOGMwIDIzLjcgNi42IDQ2LjkgMTkgNjcuMUwzMDkuNSAzMjBsLTE3MSAwTDE3MyAyNjMuOWMxMi40LTIwLjIgMTktNDMuNCAxOS02Ny4xeiIvPjwvc3ZnPgo=
[fc-class-reference]: https://img.shields.io/badge/proof%20provenance-reference-black?logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCA0NDggNTEyIiBmaWxsPSJ3aGl0ZSI+PHBhdGggZD0iTTk2IDBDNDMgMCAwIDQzIDAgOTZMMCA0MTZjMCA1MyA0MyA5NiA5NiA5NmwyODggMCAzMiAwYzE3LjcgMCAzMi0xNC4zIDMyLTMycy0xNC4zLTMyLTMyLTMybDAtNjRjMTcuNyAwIDMyLTE0LjMgMzItMzJsMC0zMjBjMC0xNy43LTE0LjMtMzItMzItMzJMMzg0IDAgOTYgMHptMCAzODRsMjU2IDAgMCA2NEw5NiA0NDhjLTE3LjcgMC0zMi0xNC4zLTMyLTMyczE0LjMtMzIgMzItMzJ6bTMyLTI0MGMwLTguOCA3LjItMTYgMTYtMTZsMTkyIDBjOC44IDAgMTYgNy4yIDE2IDE2cy03LjIgMTYtMTYgMTZsLTE5MiAwYy04LjggMC0xNi03LjItMTYtMTZ6bTE2IDQ4bDE5MiAwYzguOCAwIDE2IDcuMiAxNiAxNnMtNy4yIDE2LTE2IDE2bC0xOTIgMGMtOC44IDAtMTYtNy4yLTE2LTE2czcuMi0xNiAxNi0xNnoiLz48L3N2Zz4K
[fc-class-canonical]: https://img.shields.io/badge/proof%20provenance-canonical-black?logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCA1MTIgNTEyIiBmaWxsPSJ3aGl0ZSI+PHBhdGggZD0iTTI0My40IDIuNmwtMjI0IDk2Yy0xNCA2LTIxLjggMjEtMTguNyAzNS44UzE2LjggMTYwIDMyIDE2MGwwIDhjMCAxMy4zIDEwLjcgMjQgMjQgMjRsNDAwIDBjMTMuMyAwIDI0LTEwLjcgMjQtMjRsMC04YzE1LjIgMCAyOC4zLTEwLjcgMzEuMy0yNS42cy00LjgtMjkuOS0xOC43LTM1LjhsLTIyNC05NmMtOC0zLjQtMTcuMi0zLjQtMjUuMiAwek0xMjggMjI0bC02NCAwIDAgMTk2LjNjLS42IC4zLTEuMiAuNy0xLjggMS4xbC00OCAzMmMtMTEuNyA3LjgtMTcgMjIuNC0xMi45IDM1LjlTMTcuOSA1MTIgMzIgNTEybDQ0OCAwYzE0LjEgMCAyNi41LTkuMiAzMC42LTIyLjdzLTEuMS0yOC4xLTEyLjktMzUuOWwtNDgtMzJjLS42LS40LTEuMi0uNy0xLjgtMS4xTDQ0OCAyMjRsLTY0IDAgMCAxOTItNDAgMCAwLTE5Mi02NCAwIDAgMTkyLTQ4IDAgMC0xOTItNjQgMCAwIDE5Mi00MCAwIDAtMTkyek0yNTYgNjRhMzIgMzIgMCAxIDEgMCA2NCAzMiAzMiAwIDEgMSAwLTY0eiIvPjwvc3ZnPgo=
