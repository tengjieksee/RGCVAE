# Relational Graph Conditioned Variational Autoencoder for Molecule Design (RGCVAE)

This repository contains the code used to generate the results reported in the paper: _RGCVAE: Relational Graph Conditioned Variational Autoencoder for Molecule Design_.

# Dependencies

This project uses the `conda` environment. In the `root` folder you can find, for each model, the `.yml` file for the
configuration of the `conda` environment and also the `.txt` files for the `pip` environment. Note that some versions of
the dependencies can generate problems in the configuration of the environment. For this reason, although
the `setup.bash` file is present for the configuration of each project, it is better to configure them manually.

# Structure

The project is structured as follows:

* `data`: contains the code to execute to make the dataset;
* `results`: contains the checkpoints and the results;
* `model`: contains the code about the model;
* `utils`: contains all the utility code.

# Usage

### Data Download

First you need to download the necessary files and configuring the environment by running the following commands:

```bash
sh setup.bash install
conda activate rgcvae
```

### Data Pre-processing

In order to make de datasets type the following commands:

```bash
cd data
python make_dataset.py --dataset [dataset]
```

Where _dataset_ can be:

* qm9
* qm9_long2
* zinc
* zinc_long2

### Model Training

In order to train the model use:

```bash
python RGCVAE.py --dataset [dataset] --config '{"generation":0, "log_dir":"./results", "use_mask":false}'
```

### Model Test

In order to generate new molecules:

```bash
python RGCVAE.py --dataset [dataset] --restore results/[checkpoint].pickle --config '{"generation":1, "log_dir":"./results"}'
```

While, in order to reconstruct the molecules:

```bash
python RGCVAE.py --dataset [dataset] --restore results/[checkpoint].pickle --config '{"generation":2, "log_dir":"./results"}'
```

In order to analyze the results, we used the following
environment: [ComparisonsDGM](https://github.com/drigoni/ComparisonsDGM).

### Optimization

In order to optimize a molecule use the following command:

```bash
python RGCVAE.py --dataset zinc_long2 --restore results/[checkpoint].pickle --config '{"generation":1, "use_mask":false, "suffix":"opt", "optimization_step": 20, "number_of_generation":100, "prior_learning_rate":0.3, "use_argmax_nodes":true, "use_argmax_bonds":true}'
```

# Pre-processed datasets, Pre-trained Models and Results

[Soon we will public the pre-processed datasets, pre-trained models and generated molecules.](https://www.dropbox.com/scl/fi/urq9pnl3e190168q2qhku/RGCVAE-checkpoints.tar.gz?rlkey=inb8qwyrs8j3yfr0wa5nrnobp&dl=0)

# Information

**NOTE:** Some functions are extracted from the following
source [code](https://github.com/microsoft/constrained-graph-variational-autoencoder).

# Licenze

MIT
