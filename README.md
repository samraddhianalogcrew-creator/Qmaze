# QMaze

An interactive reinforcement learning demo that runs in the browser. A mouse starts with zero knowledge of a maze, explores by trial and error using Q-learning, and gradually learns the shortest path to the cheese. You can draw your own walls and watch it adapt in real time.

Built with vanilla JavaScript and the Canvas API. No frameworks, no build step, no dependencies.

## Demo

Open `index.html` in a browser, press **Train**, and watch the agent learn.

If you host this on GitHub Pages, add your live link here.

## How It Works

The agent uses tabular **Q-learning**. For every cell and every action (up, right, down, left) it stores a Q-value: its estimate of the long-term reward for taking that action from that cell. After every step it updates that estimate:

```
Q(s, a) <- Q(s, a) + alpha * (r + gamma * max Q(s', a') - Q(s, a))
```

- **Reward:** -1 per step, -5 for bumping into a wall or the edge, +100 for reaching the goal
- **Exploration:** epsilon-greedy. The agent takes a random action with probability epsilon, and epsilon decays after every episode down to a minimum of 0.02
- **Episodes:** each run from start to goal (or 200 steps) is one episode
- **Instant re-plan:** when you edit the maze after some training, the app sweeps the Bellman update over every cell using the known layout, so the Q-table matches the new maze at once. The mouse then restarts from the house and takes the new best route. Untick the option to make the mouse relearn by bumping into walls instead

## Reading the Visualization

| Element            | Meaning                                              |
| ------------------ | ---------------------------------------------------- |
| Teal shading       | How valuable the agent thinks a cell is (max Q-value) |
| Arrows             | The agent's currently preferred move in each cell    |
| House              | Start                                                |
| Cheese             | Goal                                                 |
| Mouse              | The agent, moving smoothly one cell per step         |

## Controls

| Control               | Effect                                                    |
| --------------------- | --------------------------------------------------------- |
| Train / Pause         | Start or stop learning                                    |
| Reset learning        | Wipe the Q-table and start over                           |
| Random walls          | Generate a random maze                                    |
| Clear walls           | Remove all walls                                          |
| Instant re-plan       | After you edit walls, the mouse updates its Q-values straight away and takes the new best route |
| Speed                 | Moves per second (default 4, so you can follow the mouse) |
| Learning rate (alpha) | How strongly new experience overwrites old estimates      |
| Discount (gamma)      | How much the agent values future rewards                  |
| Starting epsilon      | How much the agent explores at the beginning              |

Click or drag on the grid to add or remove walls.

## Things to Try

- Set gamma close to 0.5 and see how the agent becomes short-sighted
- Set alpha to 1.0 and compare the learning curve with 0.1
- Start with epsilon at 0 and see why the agent can get stuck
- Draw a maze with no valid path and watch the success rate

## Run Locally

```bash
git clone https://github.com/<your-username>/qmaze.git
cd qmaze
npx serve .
```

You can also just double-click `index.html`.

## Deploy to GitHub Pages

1. Push the repo to GitHub
2. Go to **Settings > Pages**
3. Set the source to the `main` branch and the root folder
4. Your demo will be live at `https://<your-username>.github.io/qmaze/`

## Project Structure

```
.
├── index.html   # markup, styles and the Q-learning implementation
├── README.md
└── .gitignore
```

## Ideas for Extension

- Deep Q-Network (DQN) version using TensorFlow.js
- Additional environments such as Cliff Walking or Frozen Lake
- Learning-curve chart of reward per episode
- SARSA and Q-learning comparison side by side
- Save and load mazes as JSON

## License

MIT. Add a `LICENSE` file before publishing.
