# Galaxy Ants
<a href="https://pypi.org/project/vmas"><img src="https://img.shields.io/pypi/v/vmas" alt="pypi version"></a>
[![Downloads](https://static.pepy.tech/personalized-badge/vmas?period=total&units=international_system&left_color=grey&right_color=blue&left_text=Downloads)](https://pepy.tech/project/vmas)
![tests](https://github.com/proroklab/VectorizedMultiAgentSimulator/actions/workflows/python-app.yml/badge.svg)
[![Python](https://img.shields.io/badge/python-3.8%20%7C%203.9%20%7C%203.10-blue.svg)](https://www.python.org/downloads/)
[![GitHub license](https://img.shields.io/badge/license-GPLv3.0-blue.svg)](https://github.com/proroklab/VectorizedMultiAgentSimulator/blob/main/LICENSE)

<p align="center">
<img src="https://github.com/matteobettini/vmas-media/blob/main/media/VMAS_scenarios.gif?raw=true" alt="drawing"/>  
</p>

## Welcome to Galaxy Ants!

Galaxy Ants is an aerospace intelligent control algorithm service platform. The algorithm provider uploads cutting-edge intelligent control algorithms to this platform. The algorithm user can download the algorithm to the local machine for secondary development, or use tools such as Docker, Vercel to achieve one-click deployment.


## Table of contents
- [Galaxy Ants](#vectorizedmultiagentsimulator-vmas)
  * [Welcome to VMAS!](#welcome-to-vmas)
    + [Paper](#paper)
    + [Video](#video)
  * [Table of contents](#table-of-contents)
  * [How to use](#how-to-use)
    + [Notebooks](#notebooks)
    + [Install](#install)
    + [Run](#run)
      - [RLlib](#rllib)
    + [Input and output spaces](#input-and-output-spaces)
      - [Output spaces](#output-spaces)
      - [Input action space](#input-action-space)
  * [Simulator features](#simulator-features)
  * [Creating a new scenario](#creating-a-new-scenario)
  * [Play a scenario](#play-a-scenario)
  * [Rendering](#rendering)
    + [Plot function under rendering](#plot-function-under-rendering)
    + [Rendering on server machines](#rendering-on-server-machines)
  * [List of environments](#list-of-environments)
    + [VMAS](#vmas)
       - [Main scenarios](#main-scenarios)
       - [Debug scenarios](#debug-scenarios)
    + [MPE](#mpe)
  * [TODOS](#todos)


## How to use
### Notebooks
-  [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/10R6KIRG5grpBFBDUI5njTcKvZ2rqsaWd?usp=share_link) &ensp; **Running oline**.
 Here is a simple notebook that you can run to create, step and render a senario using multi-agent reinforcement learning algorithm.



### Install

To install the simulator, you can use pip to get the latest release:
```
pip install vmas
```
If you want to install the current master version (more up to date than latest release), you can do:
```
git clone https://github.com/proroklab/VectorizedMultiAgentSimulator.git
cd VectorizedMultiAgentSimulator
pip install -e .
```
By default, vmas has only the core requirements. Here are some optional packages you may want to install:
```
# Training
pip install "ray[rllib]"==2.2 # We support versions "ray[rllib]<=2.2,>=1.13"
pip install torchrl

# Logging
pip installl wandb 

# Save renders
pip install opencv-python moviepy

# Tests
pip install pytest pyyaml pytest-instafail tqdm
```

### Run 

To use the simulator, simply create an environment by passing the name of the scenario
you want (from the `scenarios` folder) to the `make_env` function.
The function arguments are explained in the documentation. The function returns an environment
object with the OpenAI gym interface:

Here is an example:
```
 env = vmas.make_env(
        scenario="waterfall", # can be scenario name or BaseScenario class
        num_envs=32,
        device="cpu", # Or "cuda" for GPU
        continuous_actions=True,
        wrapper=None,  # One of: None, vmas.Wrapper.RLLIB, and vmas.Wrapper.GYM
        max_steps=None, # Defines the horizon. None is infinite horizon.
        seed=None, # Seed of the environment
        dict_spaces=False, # By default tuple spaces are used with each element in the tuple being an agent.
        # If dict_spaces=True, the spaces will become Dict with each key being the agent's name
        **kwargs # Additional arguments you want to pass to the scenario initialization
    )
```
A further example that you can run is contained in `use_vmas_env.py` in the `examples` directory.

#### RLlib

To see how to use VMAS in RLlib, check out the script in `examples/rllib.py`.

### Input and output spaces

VMAS uses gym spaces for input and output spaces. 
By default, action and observation spaces are tuples:
```python
spaces.Tuple(
    [agent_space for agent in agents]
)
```
When creating the environment,  by setting `dict_spaces=True`, tuples can be changed to dictionaries:
```python
spaces.Dict(
  {agent.name: agent_space for agent in agents}
)
```

#### Output spaces

If `dict_spaces=False`, observations, infos, and rewards returned by the environment will be a list with each element being the value for that agent.

If `dict_spaces=True`, observations, infos, and rewards returned by the environment will be a dictionary with each element having key = agent_name and value being the value for that agent.

Each agent observation in either of these structures is a tensor with shape `[num_envs, observation_size]`, where `observation_size` is the size of the agent's observation.

Each agent reward in either of these structures is a tensor with shape `[num_envs]`.

Each agent info in either of these structures is a dictionary where each entry has key representing the name of that info and value a tensor with shape `[num_envs, info_size]`, where `info_size` is the size of that info for that agent.

Done is a tensor of shape `[num_envs]`.


#### Input action space
  
Each agent in vmas has to provide an action tensor with shape `[num_envs, action_size]`, where `num_envs` is the number of vectorized environments and `action_size` is the size of the agent's action.

The agents' actions can be provided to the `env.step()` in two ways:
- A **List** of length equal to the number of agents which looks like `[tensor_action_agent_0, ..., tensor_action_agent_n]`
- A **Dict** of length equal to the number of agents and with each entry looking like `{agent_0.name: tensor_action_agent_0, ..., agent_n.name: tensor_action_agent_n}`

Users can interchangeably use either of the two formats and even change formats during execution, vmas will always perform all sanity checks. 
Each format will work regardless of the fact that tuples or dictionary spaces have been chosen.

                                        |
