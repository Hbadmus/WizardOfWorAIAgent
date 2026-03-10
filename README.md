

# Wizard of Wor – DDQN AI Agent

**Tech:** Python, PyTorch, Gymnasium, OpenAI Gym  
**Role:** Reward Engineering, Agent Behavior Analysis, Technical Documentation  
**Type:** Collaborative Research Project

---

## Overview

Trained a Double Deep Q-Network (DDQN) agent to play Wizard of Wor autonomously, achieving near-complete level completion through strategic enemy elimination and maze navigation. The core challenge wasn't the model architecture. It was designing a reward structure that produced intelligent, deliberate behavior rather than passive survival.

---

## Reward System Design

The reward structure went through multiple iterations. Early versions produced an agent that avoided enemies effectively but rarely engaged — optimizing for survival rather than progression. The design problem became clear: the agent needed to be incentivized to win, not just to stay alive.

### Design Goals
- Discourage passive play and stalling
- Reward aggressive, strategic enemy elimination
- Penalize unnecessary risk without discouraging engagement

### Key Mechanics

**Survival Penalty**  
A small continuous time penalty was applied each step to prevent the agent from stalling in safe zones. This forced forward movement and engagement rather than passive avoidance.

**Score Amplification**  
Kill rewards were scaled based on enemy type and context. Higher-value enemies yielded disproportionately larger rewards to train the agent to prioritize threat elimination strategically, mirroring how a skilled human player would approach the game.

**Death Penalty**  
A significant negative reward on death to reinforce risk awareness without overriding the incentive to engage enemies.

---

## Iteration Process

Each training run was analyzed for behavioral patterns before adjusting design parameters. Key failure modes identified across iterations:

- **Stalling behavior:** agent camping in corridors. Fixed by increasing the survival time penalty.
- **Indiscriminate aggression:** agent charging high-value enemies without clearing lower threats first. Fixed by tuning kill reward scaling relative to enemy proximity.
- **Maze navigation loops:** agent revisiting cleared areas instead of progressing. Addressed by adjusting score amplification to reward level progression.

Design changes were always driven by observed behavior, not assumptions. If the agent wasn't doing something, the reward structure wasn't asking it to.

---

## Results

The agent achieved near-complete level completion across consistent training runs, demonstrating strategic enemy prioritization and efficient maze traversal. Remaining failure cases occurred primarily in late-level scenarios with simultaneous multi-enemy encounters.

---

## What I Learned

Reward engineering is fundamentally a design problem. The math matters, but the harder question is always: *what behavior do you actually want, and are your rules producing it?* Watching the agent fail in unexpected ways — and tracing that failure back to an incentive misalignment — was the most valuable part of the process.


## Authors

- [Sharyq Siddiqi](https://www.github.com/ryqshaw)
- [Shishir Pokhrel](https://www.github.com/pokhrel-sh)
- [Hakim Badmus](https://www.github.com/Hbadmus)
- [Sunil Williams](https://github.com/sunilwilliams4)

## Getting Started

Project running on Python 13\
To get started run `./setup.sh` on Linux/Mac, or `.\setup.bat` on Windows to install these Programs(Dependencies Included):\
ale-py==0.11.0\
gymnasium==1.1.1\
numpy==2.2.6\
pygame==2.6.1\
torch==2.7.0

when running `main.py`, you can set the model ran had on line 36 with `dqn.load_state_dict(torch.load("nn.pth"))`, where nn.pth is default model.\

when running `training.py`, and wanting to make your own model, you can change the factors and run this function `train(batch_size=64, gamma=0.999, epsilon=1, decay=.99999, max_episodes=10000, min_epsilon=0.1, max_episode_steps=18000, load_checkpoint = False)`. default train function is on line 208.\

Model is default saved as nn.pth

## Acknowledgements

 - [Arcade Learning Enviorment](https://ale.farama.org/)
 - [Gymnasium](https://gymnasium.farama.org/)

