Making Formal Verification Trustworthy via Proof Generation
-----------------------------------------------------------

Welcome! This repository contains supplemental materials for our paper, including:
- A formalization of reachability in Metamath (`theory/kore-reachability.mm`),
- Our implementation for the proof generation procedure in the paper,
- Scripts for the evaluation section.

## Dependencies

Our tool depends on the following software:
- PyPy 3.7+ ([https://www.pypy.org/download.html](https://www.pypy.org/download.html))
- Python 3.7+ ([https://www.python.org/downloads/](https://www.python.org/downloads/))
- Metamath ([http://us.metamath.org/#downloads](http://us.metamath.org/#downloads))
- A modified version of the K framework

After Python 3 and PyPy 3 are installed, run the following to install required packages:
```
python3 -m pip install -r requirements.txt
pypy3 -m pip install -r requirements.txt
```

To build the modified version of the K framework, first clone the submodule `deps/k`:
```
git submodule update --init --recursive --depth 1
```

Then change directory to `deps/k`, and follow instructions
in [https://github.com/kframework/k](https://github.com/kframework/k) to build K.

## Reachability Formalization

Details of our reachability lemmas can be found in the Metamath database `theory/kore-reachability.mm`.  
To verify all the proofs, run
```
metamath 'read "theory/prelude.mm"' 'verify proof *' quit
```
which is expected to show the following output
```
...
13560360 bytes were read into the source buffer.
The source has 3494 statements; 242 are $a and 692 are $p.
No errors were found.  However, proofs were not checked.  Type VERIFY PROOF *
if you want to check them.
MM> verify proof *
0 10%  20%  30%  40%  50%  60%  70%  80%  90% 100%
..................................................
All proofs in the database were verified in 6.29 s.
```

## Evaluation

All K specifications used in the evaluation can be found in `examples/pldi22/specs`.

To reproduce the evaluation results, run the following
```
cd examples/pldi22
make all
make verify
make compress
python3 stats.py
```
The last command will produce a Latex tabular containing
statistics similar to the table of evaluation results in the paper.
