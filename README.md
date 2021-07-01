# Mastering Mini Atari with Discrete World Models

Pytorch implementation of [Mastering Atari with Discrete World Models](https://arxiv.org/abs/2010.02193)<br>

## Running experiments
1) In tests folder, mdp.py and pomdp.py have been setup for experiments with MinAtar environments. All default hyper-parameters used, are stored in a dataclass in [config.py](https://github.com/RajGhugare19/dreamerv2/blob/b6d65b8af7f91ae106c5b0cc11e29a2247dfa233/dreamerv2/training/config.py#L9). To run dreamerv2 with default HPs on POMDP breakout and cuda device :
  ```
  python pomdp.py --env breakout --device cuda
  ``` 
  - Training curves are logged using wandb. 
  - A `results` folder will be localy created locally to store models while training.
    - `/env_name+_env_id_+pomdp/models`   

2) Experimenting on other environments(using gym-api) can be done by adding another hyper-parameter dataclass in [config.py](https://github.com/RajGhugare19/dreamerv2/blob/b6d65b8af7f91ae106c5b0cc11e29a2247dfa233/dreamerv2/training/config.py#L9). <br>

## Evaluating saved models
TO-DO

## Code structure:
- `test`
  - `pomdp.py` run MinAtar experiments with partial observability.
  - `mdp.py` run MinAtar experiments.
  - `eval.y` evaluate saved agents.
- `dreamerv2` dreamerv2 plus dreamerv1 and combinations thereof.
  - `models` neural network models.
    - `actor.py` discrete action model.
    - `dense.py` fully connected neural networks.
    - `pixel.py` convolutional encoder and decoder.
    - `rssm.py` recurrent state space model.
  - `training`
    - `config.py` hyper-parameter dataclass.
    - `trainer.py` training class.
    - `evaluator.py` evaluation class.
  - `utils`
    - `algorithm.py` lambda return function.
    - `buffer.py` replay buffers.
    - `module.py` neural network parameters utils
    - `rssm.py` recurrent state space model utils
    - `wrapper.py` gym api and pomdp wrappers for MinAtar     

## Hyper-Parameter description:

Since there are many hyper-parameters, I am sharing my understanding, based on the experiments and reading related papers, on some of them.<br>
- `train_every`: number of frames to skip while training.
- `collect_intervals`: number of batches to be sampled from buffer, at every "train-every" iteration.
- `seq_len`: length of trajectory sequence to be sampled from buffer.
- `embedding_size`: size of embedding vector that is output by observation encoder.
- `rssm_node_size`: size of hidden layers of temporal posteriors and priors.
- `deter_size`: size of deterministic part of recurrent state.
- `stoch_size`: size of stochastic part of recurrent state.
- `class_size`: number of classes for each categorical random variable
- `category_size`: number of categorical random variables.
- `horizon`: horizon for imagination in future latent state space.
- `kl_balance_scale`: scale for kl balancing.
- `actor_entropy_scale` scale for policy entropy regularization in latent state space.

## Acknowledgments
Awesome Environments used for testing:

- MinAtar by kenjyoung : [https://github.com/kenjyoung/MinAtar](https://github.com/kenjyoung/MinAtar)<br>
- minigrid by maximecb : [https://github.com/maximecb/gym-minigrid](https://github.com/maximecb/gym-minigrid)<br>

This code is built on and heavily inspired by the following works:

- danijar's (author of Dreamer-v2) Tensorflow implementation : [https://github.com/danijar/dreamer](https://github.com/danijar/dreamer)<br>
- juliusfrost's Dreamer-v1 pytorch implementation : [https://github.com/juliusfrost/dreamer-pytorch](https://github.com/juliusfrost/dreamer-pytorch)<br>
- yusukeurakami's Dreamer-v1 pytorch implementation: [https://github.com/yusukeurakami/dreamer-pytorch](https://github.com/yusukeurakami/dreamer-pytorch)<br>
- alec-tschantz's  PlaNet pytorch implementation : [https://github.com/alec-tschantz/planet](https://github.com/alec-tschantz/planet)<br>
- qlan3's gym-games : [https://github.com/qlan3/gym-games](https://github.com/qlan3/gym-games)

Thanks for all the great work :)
