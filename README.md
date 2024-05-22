# TurboGP

TurboGP is a Python implementation of the Genetic Programming (GP) framework [1]. It is specifically designed for machine learning tasks. It supports many modern and popular GP features such as:

* Parallel processing: TurboGP can take advantage of systems with multiple CPU cores/threads in different ways, e.g. parallel evaluation of individuals in the population, or island subpopulations split across different CPUs along migration operations.

* On-line learning. TurboGP provides a variant of steady state population dynamics, specifically tailored to increase efficiency under mini-batch based learning/evolution. This method can significantly accelerate learning when dealing with large datasets [2].

* Spatially distributed populations. TurboGP supports models that allocate individuals in toroidal grid arrangements (aka cellular GP) [3], as well as provides export, import and migration operations to allow the implementation of multi-population (island) models [4].

* Layers of different types of nodes. TurboGP allows the representation and recombination of GP trees with different abstraction (nodes) layers. These models are specially useful in high dimensional learning problems [5-7].

* Batteries included. TurboGP comes with quick run example scripts, as well as a script to generate datasets based on an assortment of classical artificial regression problems, to readily test TurboGP. 

Besides the features mentioned above, TurboGP also implements different crossover operations (_protected_ crossover variants), it allows to graphically display the individuals/models generated, and allows live plotting of the fitness and diversity evolution.

![TurboGP](Preview.png)

## Getting Started

TurboGP ships with several jupyter notebooks that explain in detail how to use the library. The notebooks cover a simple regression example, under different scenarios (offline learning, online learning, parallel CPU usage), as well as an example on a multi-layered GP for image denoising. Other examples include binary classification for classic UCI repository datasets [8], examples on how to use TurboGP from the OS shell (CLI), among others. There is also a notebook that covers more in depth the inner workings of TurboGP (core classes and methods).

### Prerequisites

TurboGP should run on any version of Python >= 3.6.
Required libraries (most of these ship by default in recent conda distributions):

- numpy 
- TQDM (to display progressbar)
- matplotlib (to live display fitness/diversity progress, as well as for models' (trees) viz)

Optional:

- numba (to speed-up evolutionary runs; can be activated or deactivated in primitives sets files LowLever.py, Mezzanine.py, etc.) 
- wget, pandas (to run UCI repository examples)

For models' visualization (plotting generated trees)*:

- networkx, pygraph and pygraphviz 



### Installing

You can clone the repo and run one of the included Jupyter notebooks or example scripts, to verify that the library works properly in your system. 

## Authors

* **Lino Rodriguez-Coayahuitl** - [l1n0b1](https://github.com/l1n0b1)

See also the list of [contributors](https://github.com/l1n0b1/TurboGP/AUTHORS) who participated in this project.

## License

This project is licensed under The GNU General Public License v3.0  - see the [LICENSE](LICENSE) file for details

## Changelog

### Version 1.3.1

Minor release. Changes:

- Added documentation to illustrate some of the included artificial regression problems.
- Added scripts to run some of the examples (Keijzer 12 single population vs distributed) described in the TurboGP article (see below, in Citation).
- Switched from Python standard math library + numba to numpy to implement some primitives definitions (for speed up).
- Other minor changes, updates and bug fixes (see merge log for detailed info).

### Version 1.3

Third release. New features:

- Added numeric mutation genetic operation [13].
- Added RegressorLS GP individual (SimpleRegresor with Linear Scaling [14].
- Added script to automatize multiple runs of different GP setups.
- Added collection of artificial regression datasets.
- Cleaned coded in general and other minor corrections.

### Version 1.2

Second release. New features:

- Crossover is now debiased.
- Added BinaryClassifier evolvable individual class.
- Added GeneticProgram class, that allows to instantiate and launch complete GP runs through a scikit[9]-alike interface.
- Added CLI that allows to launch GP runs (settings are defined in JSON files, while datasets are read in pickled files).
- Added GeneticProgramD class, aimed at deploying multi-population GP that can take advantage of multicore CPU systems.
- Added examples that illustrate on all the new features (BinaryClassifier, scikitlearn-alike interface, CLI, etc.)


### Version 1.0

First commit. Features included:
- Parallel individuals' evaluation.
- Low, mezzanine, high level primitives support.
- Genetic operations: subtree crossover, protected subtree crossover, subtree mutation, point mutation, etc.
- Migration operations: import, export, etc.
- Cellular and RecombinativeHillClimbing population models.
- Steady State dynamics with support for on-line learning.
- SimpleRegresor class for scalar regression .
- NonConvFilter, NonConvolutionalMezzanineFilter classes for image denoising.
- Live training, testing fitness, and diversity plotting; generated models visualization.


## TO-DO

Minor improvements required:

- Add _simplification_ and _prunning_ techniques.
- Parallelize genetic operations (only evaluations are carried in parallel in multiple CPU systems).
- Add _forest_-based GP individuals class, and examples (e.g. GP autoencoder).

## Roadmap

Major upcoming or planned features:

- Cooperative Co-Evolutionary GP models [10].
- Add support for local search (_memetic_ [11]) GP enhanced variants.
- Add support for subroutine discovery (cooperative models, ADFs [12], etc.)
- Provide compatibility with PyPy for faster runtimes.

## Citation

If you find TurboGP useful, and employ it in your research, you can cite its official draft:

[Rodriguez-Coayahuitl, L., Morales-Reyes, A., & Escalante, H. J. (2023). TurboGP: A flexible and advanced python based GP library. arXiv preprint arXiv:2309.00149.](https://arxiv.org/pdf/2309.00149)

You will also find there some benchmarks of its features as well as a basic usage example code.

For BibTeX users, you can include this entry in your `.bib` file.

```
@article{rodriguez2023turbogp,
  title={TurboGP: A flexible and advanced python based GP library},
  author={Rodriguez-Coayahuitl, Lino and Morales-Reyes, Alicia and Escalante, Hugo Jair},
  journal={arXiv preprint arXiv:2309.00149},
  year={2023}
  url = {https://github.com/l1n0b1/TurboGP}
}
```

---


## References

[1] Koza, J. R., & Koza, J. R. (1992). Genetic programming: on the programming of computers by means of natural selection (Vol. 1). MIT press.

[2] Rodriguez-Coayahuitl, L., Morales-Reyes, A., & Escalante, H. J. (2019). Evolving autoencoding structures through genetic programming. Genetic Programming and Evolvable Machines, 20(3), 413-440.

[3] Petty, C. C. (1997). Diffusion (cellular) models. Handbook of evolutionary Computation.

[4] Martin, W. N., Lienig, J., & Cohoon, J. P. (1997). C6. 3 Island (migration) models: evolutionary algorithms based on punctuated equilibria. B ack et al. BFM97], Seiten C, 6, 101-124.

[5] Al-Sahaf, H., Song, A., Neshatian, K., & Zhang, M. (2012). Two-tier genetic programming: Towards raw pixel-based image classification. Expert Systems with Applications, 39(16), 12291-12301.

[6] Evans, B., Al-Sahaf, H., Xue, B., & Zhang, M. (2018, July). Evolutionary deep learning: A genetic programming approach to image classification. In 2018 IEEE Congress on Evolutionary Computation (CEC) (pp. 1-6). IEEE.

[7] Rodriguez-Coayahuitl, L., Morales-Reyes, A., & Escalante, H. J. (2019, November). A Comparison among Different Levels of Abstraction in Genetic Programming. In 2019 IEEE International Autumn Meeting on Power, Electronics and Computing (ROPEC) (pp. 1-6). IEEE.

[8] Dua, D. and Graff, C. (2019). UCI Machine Learning Repository [http://archive.ics.uci.edu/ml]. Irvine, CA: University of California, School of Information and Computer Science. 

[9] Scikit-learn: Machine Learning in Python, Pedregosa et al., JMLR 12, pp. 2825-2830, 2011.

[10] Rodriguez-Coayahuitl, L., Morales-Reyes, A., Escalante, H. J., & Coello, C. A. C. (2020, September). Cooperative co-evolutionary genetic programming for high dimensional problems. In International Conference on Parallel Problem Solving from Nature (pp. 48-62). Springer, Cham.

[11] Emigdio, Z., Trujillo, L., Schütze, O., & Legrand, P. (2014). Evaluating the effects of local search in genetic programming. In EVOLVE-A Bridge between Probability, Set Oriented Numerics, and Evolutionary Computation V (pp. 213-228). Springer, Cham.

[12] Koza, J. R. (1994). Genetic programming II: automatic discovery of reusable programs. MIT press.

[13] Evett, M., & Fernandez, T. (1998). Numeric mutation improves the discovery of numeric constants in genetic programming. Genetic Programming, 66-71.

[14] Keijzer, M. (2003, April). Improving symbolic regression with interval arithmetic and linear scaling. In European Conference on Genetic Programming (pp. 70-82). Springer, Berlin, Heidelberg.
