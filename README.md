# rlmaster

Environments and RL algorithms. 

## Environment
An environment is defined by:

- Simulator: an object of `type BaseSimulator` that simulates the effect of agent's actions in the environment and provides
             observations.

- Initializer: an object of type `BaseInitializer` that defines how the epsiode should be initialized.

- Observer: an object of `type BaseObserver` that choses the desired representation from the simulator. It is useful when 
            it is required to train an agent in the same environment but with different observations (for eg: training with
            pixels or with state features)
            
- Rewarder: an object of `type BaseRewarder` that describes the reward function. It is useful when the agent needs to be trained
            on the same environment but with different reward functions. 
            
- ActionProcessor: an object of `type BaseAction` that defines functions that process the action. Generally simulator works
                   by applying continous forces/torque, however the desired action space might be discrete or continuous. 
                   `BaseAction` objects allow the user to easily switch between different action spaces. 
                   
### Interactive Mode
To run environments in interactive mode, a function mapping the keyboard inputs into commands supplied to the agent must be defined. This function is typically called, `str2action` in `rlmaster` repository. The environment can be run in interactive mode in the following way:

```python
from envs.mujoco_envs import move_single_env
env = move_single_env.get_environment(actType='ContinuousAction', imSz=480)
env.interactive(move_single_env.str2action)
```
You can use the commands, `w, s, d, a` to move the agent and `q` to quit the interactive mode.

                   

##Environment in openAI gym format

```python
from envs import move_agent
from core import gym_wrapper
env = move_agent.get_environment()
gymEnv = gym_wwapper.GymWrapper(env)
```

## Visualizing the enviornment
```python
import env_utils
#Create a visualization object
envVis = env_utils.BaseEnvVis(env) #See source for more options
#Visualize random exploration of the environment
envVis.vis_exploration()
#Visualize how the env looks on reset
envVis.vis_resets()
#Visualize "touch" along with random exploration
envVis.vis_exploration_touch()
```

## Notes on setting environment with mujoco

If there is a static body that doesnot move, then set it's `body_pos`. If there is a body that can move
then set it's `qpos`.




                   
            



