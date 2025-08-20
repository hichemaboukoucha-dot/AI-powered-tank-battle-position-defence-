# AI-powered-tank-battle-position-defence-
A Pygame-based particle simulation where circles aim to reach a goal while shooting at defending X points, using AI to target based on predicted enemy vulnerability. Features dynamic halos, trails, S/V metrics, and a commentary system. Pyodide-compatible for browser execution.
# Particle Simulation

## Overview
This is a Pygame-based particle simulation that models a dynamic interaction between two teams of particles: **Circles** and **X Points**. Circles aim to reach a goal at the bottom center of the screen, while X Points defend it by minimizing the Circles' progress. The simulation incorporates:

- **Team Dynamics**: Circles and X Points operate based on team performance metrics (Strength/Vulnerability, or S/V), calculated using danger (`J`), cohesion (`D`), probability of being targeted (`cp`), and heat functions (`H`).
- **Shooting Mechanism**: Circles can shoot at X Points every 1 second, predicting targets using a simple AI that maximizes the X Points' vulnerability (`V`) by simulating a loss of cohesion from shots.
- **Halo Radii**: Each particle has a dynamic halo radius (`Hr`) visualizing its influence, based on `J`, `D`, and `cp`, without assuming direct enemy detection.
- **Commentary System**: A narrative system describes each particle’s "feelings" (e.g., pressure, exposure, or team unity) based on its environment, cycling through particles every 3 seconds.
- **Visual Features**: Trails show particle paths, and orange lines indicate shots. The simulation can be paused/resumed with the spacebar.
- **Performance Tracking**: Tracks S/V scores over time for both teams, displayed on-screen.

The code is designed to run in a browser using Pyodide, ensuring no local file I/O or network calls.

## Requirements
- **Python 3.8+** (for local execution)
- **Pygame**: For rendering the simulation (`pip install pygame`)
- **NumPy**: For vector calculations (`pip install numpy`)
- **Pyodide**: For browser-based execution (no local installation needed; see below for browser setup)
- **Browser**: For Pyodide, use a modern browser (e.g., Chrome, Firefox)

## Setup
### Running Locally
1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd particle-simulation
   ```
2. Install dependencies:
   ```bash
   pip install pygame numpy
   ```
3. Run the simulation:
   ```bash
   python particle_simulation.py
   ```

### Running in Browser (Pyodide)
1. Host the `particle_simulation.py` file on a web server or use a Pyodide-compatible environment (e.g., a Jupyter notebook with Pyodide kernel).
2. Ensure the code is loaded in a Pyodide environment, which handles Pygame rendering in the browser.
3. Open the browser console to verify the simulation runs without errors.

## Usage
- **Controls**:
  - **Spacebar**: Pause or resume the simulation.
  - **Close Window**: Exit the simulation.
- **Simulation Mechanics**:
  - **Circles** (red): Move toward the goal (green circle at bottom center), shooting at X Points to maximize their vulnerability.
  - **X Points** (blue): Defend the goal by targeting Circles to minimize their S/V score.
  - **Shooting**: Circles shoot every 1 second, pushing X Points with a velocity boost. Shots are visualized as orange lines.
  - **Commentary**: Text at the bottom describes one particle’s state (e.g., threat level, team cohesion) every 3 seconds.
  - **Trails**: Fading trails show particle movement history.
  - **S/V Scores**: Displayed at the top, showing team performance (Strength/Vulnerability).
- **Goal**: Circles aim to maximize their S/V by reaching the goal, while X Points aim to minimize the Circles’ S/V.

## Code Structure
- **particle_simulation.py**: Main script containing:
  - `Particle` class: Manages position, velocity, trails, and shooting timers.
  - Core functions: `compute_distance`, `danger_function`, `cohesion`, `probability_chosen`, `vulnerability`, `heat_function`, `strength`, `team_performance`, `halo_radius`, `choose_target`, `predict_v_after_shot`, `get_commentary`.
  - Game loop: `update_loop`, `draw`, `setup`, `main` (using `asyncio` for Pyodide compatibility).
- Key constants: `WIDTH`, `HEIGHT`, `FPS`, `PARTICLE_RADIUS`, `HALO_RADIUS_SCALE`, `SHOOT_COOLDOWN`, `PUSH_STRENGTH`.

## How It Works
- **Team Performance (S/V)**: Combines strength (`S`, based on proximity to the goal and feedback) and vulnerability (`V`, based on cohesion and enemy proximity).
- **Shooting AI**: Circles predict the next vulnerability (`V`) of X Points by simulating a shot’s effect (pushing the target), choosing the target that maximizes `V`.
- **Halo Radii**: Visualized as yellow rings, representing a particle’s influence based on danger, cohesion, and targeting probability.
- **Commentary**: Describes particles’ "feelings" (e.g., "Feels strong pressure from nearby threats") using normalized metrics, avoiding direct enemy detection references.
- **Pyodide Compatibility**: Uses `asyncio` for frame updates and avoids file I/O or network calls.

## Future Improvements
- Add mouse interaction to move the goal or select particles for commentary.
- Plot S/V history over time using a visualization library (e.g., matplotlib or canvas-based plotting).
- Introduce obstacles or new particle types for more complex dynamics.
- Enhance shooting with cooldown variations or different effects (e.g., slowing targets).
- Export simulation data (e.g., S/V history) as text for analysis.

## Contributing
Feel free to fork the repository, submit issues, or create pull requests. Please ensure any changes maintain Pyodide compatibility and include clear documentation.

## License
MIT License. See `LICENSE` file for details.
