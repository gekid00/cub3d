# cub3D

A 3D graphical engine inspired by Wolfenstein 3D, built as part of the 42 school curriculum.
The program renders a first-person perspective inside a maze defined by a `.cub` map file,
using raycasting with the DDA (Digital Differential Analyzer) algorithm.

## Technologies

- **Language:** C (C89/90, compiled with `-Wall -Wextra -Werror`)
- **Graphics:** MiniLibX (X11)
- **Build:** GNU Make, GCC

## Build

```sh
make        # Compile the project
make clean  # Remove object files
make fclean # Remove object files and executable
make re     # Full rebuild
```

## Usage

```sh
./cub3D <path_to_map.cub>
```

**Example:**

```sh
./cub3D test_maps/valid/map.cub
```

### Map format (`.cub`)

The map file must contain:
- Cardinal texture paths (`NO`, `SO`, `WE`, `EA`)
- Floor and ceiling RGB colors (`F`, `C`)
- A valid enclosed map using `1` (wall), `0` (floor), and a player spawn (`N`/`S`/`E`/`W`)

### Controls

| Key          | Action          |
|--------------|-----------------|
| `W` / `S`    | Move forward / backward |
| `A` / `D`    | Strafe left / right |
| Left / Right arrows | Rotate camera |
| `ESC`        | Quit            |

## Key Technical Concepts

- **Raycasting (DDA):** For each screen column, a ray is cast into the 2D map grid. The DDA algorithm efficiently determines wall intersections to calculate perpendicular distances, which are used to derive wall strip heights and produce a 3D perspective.
- **Texture mapping:** Wall textures are selected based on the cardinal direction of the hit surface and sampled according to the ray's exact hit position.
- **Map parsing and validation:** The `.cub` file is fully validated, including wall enclosure checks via flood fill, duplicate detection, and color/path verification.
