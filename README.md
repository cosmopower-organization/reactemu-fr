# `ReACTemu-f(R)`

`ReACTemu-f(R)` is an emulator of the nonlinear correction to the matter power spectrum for `f(R)` gravity with massive neutrinos. It is built using the [`CosmoPower`](https://github.com/alessiospuriomancini/cosmopower) neural emulation framework to emulate the predictions of the [`ReACT`](https://github.com/nebblu/ACTio-ReACTio) code.

Since `ReACTemu-f(R)` is a `CosmoPower` network, the syntax to use this emulator is the same as any other `CosmoPower` emulator. We report an example below, and refer to the `CosmoPower` [repository](https://github.com/alessiospuriomancini/cosmopower), [documentation](https://alessiospuriomancini.github.io/cosmopower/) and original `CosmoPower` [paper](https://doi.org/10.1093/mnras/stac064) for details on the emulation framework.


## Installation

To use `ReACTemu-f(R)` you should first install `CosmoPower`. This is most conveniently done inside a `Conda` environment:

    conda create -n cp_env python=3.7 pip && conda activate cp_env

Once inside the environment, you can install `CosmoPower` with

    pip install cosmopower


## Using `ReACTemu-f(R)`

To use `ReACTemu-f(R)` you can simply instantiate a `cosmopower_NN` class and load the `.pkl` file storing the emulator:

```py
import cosmopower as cp

# load ReACTemu-f(R)
cp_nn = cp.cosmopower_NN(restore=True, 
                         restore_filename='/path/to/reactemu-fr')

# create a dict of cosmological parameters
params_fr =  {'Omega_m':        [0.3164],
              'Omega_b':        [0.04966],
              'H_0':            [67.1],
              'n_s':            [0.9647],
              'A_s':            [2.1031e-9],
              'f_R0':           [1e-6],
              'Omega_nu':       [0.0014],
              'z':              [0.],
              }

# predictions (= forward pass through the network) -> 10^predictions
spectra = cp_nn.ten_to_predictions_np(params_fr)
```


## Citation

If you use `ReACTemu-f(R)` please cite its release [paper](https://arxiv.org/abs/2305.06350) as well as the `CosmoPower` release [paper](https://doi.org/10.1093/mnras/stac064):

    @article{SpurioMancini2023,
        author = "Spurio Mancini, A. and Bose, B.",
        title = "{On the degeneracies between baryons, massive neutrinos and f(R) gravity in Stage IV cosmic shear analyses}",
        eprint = "2305.06350",
        archivePrefix = "arXiv",
        primaryClass = "astro-ph.CO",
        month = "5",
        year = "2023"
    }

    @article{SpurioMancini2022,
             title={CosmoPower: emulating cosmological power spectra for accelerated Bayesian inference from next-generation surveys},
             volume={511},
             ISSN={1365-2966},
             url={http://dx.doi.org/10.1093/mnras/stac064},
             DOI={10.1093/mnras/stac064},
             number={2},
             journal={Monthly Notices of the Royal Astronomical Society},
             publisher={Oxford University Press (OUP)},
             author={Spurio Mancini, Alessio and Piras, Davide and Alsing, Justin and Joachimi, Benjamin and Hobson, Michael P},
             year={2022},
             month={Jan},
             pages={1771–1788}
             }
 
# License

``ReACTemu-f(R)`` is released under the GPL-3 license (see [LICENSE](https://github.com/cosmopower-organization/reactemu-fr/blob/main/LICENSE)) subject to the non-commercial use condition (see [LICENSE_EXT](https://github.com/cosmopower-organization/reactemu-fr/blob/main/LICENSE_EXT)).

    ReACTemu-f(R)
    Copyright (C) 2023 A. Spurio Mancini & contributors

    This program is released under the GPL-3 license (see LICENSE),
    subject to a non-commercial use condition (see LICENSE_EXT).

    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

