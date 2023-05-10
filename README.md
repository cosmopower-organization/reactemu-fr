# `ReACTemu-f(R)`

`ReACTemu-f(R)` is an emulator of the nonlinear correction to the matter power spectrum for `f(R)` gravity with massive neutrinos. It is built using the [`CosmoPower`](https://github.com/alessiospuriomancini/cosmopower) neural emulation framework to emulate the predictions of the [`ReACT`](https://github.com/nebblu/ACTio-ReACTio) code.

Since `ReACTemu-f(R)` is a `CosmoPower` network, the syntax to use this emulator is the same as any other `CosmoPower` emulator. We report an example below, and refer to the `CosmoPower` [repository](https://github.com/alessiospuriomancini/cosmopower), [documentation](https://alessiospuriomancini.github.io/cosmopower/) and original `CosmoPower` [paper](https://doi.org/10.1093/mnras/stac064) paper for details on the emulation framework.


## Installation

To use `ReACTemu-f(R)` you should first install `CosmoPower`. This is most conveniently done inside a `Conda` environment:

    conda create -n cp_env python=3.7 pip && conda activate cp_env

Once inside the environment, you can install `CosmoPower` with

    pip install cosmopower


## Using `ReACTemu-f(R)`

To use `ReACTemu-f(R)` you can simply instantiate a `cosmopower_NN` emulator and loading the `.pkl` file storing `ReACTemu-f(R)`:


    ```py
    import cosmopower as cp

    # load pre-trained NN model: maps cosmological parameters to CMB TT log-C_ell
    cp_nn = cp.cosmopower_NN(restore=True, 
                             restore_filename='/path/to/reactemu-fr')

    # create a dict of cosmological parameters
    params = {'omega_b': [0.0225],
              'omega_cdm': [0.113],
              'h': [0.7],
              'tau_reio': [0.055],
              'n_s': [0.96],
              'ln10^{10}A_s': [3.07],
             }

    # predictions (= forward pass through the network) -> 10^predictions
    spectra = cp_nn.ten_to_predictions_np(params)
    ```
