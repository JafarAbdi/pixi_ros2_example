# ROS 2 pixi example

## Installation

```bash
pixi run setup-colcon
```

## Usage

```bash
pixi shell -e jazzy
pixi shell -e humble
```

## ament_cmake_pkg

This is an example package generate from `ros2 pkg` cli

```bash
ros2 pkg create --build-type ament_cmake ament_cmake_pkg
```

## ament_python_pkg

This is an example package generate from `ros2 pkg` cli

```bash
ros2 pkg create --build-type ament_python ament_python_pkg
```

## Replicating the environment

```bash
pixi init
# Dependencies
pixi add colcon-common-extensions colcon-mixin cmake ninja mold sccache
# Tasks
pixi task add build "colcon build"
pixi task add test "colcon test" --depends-on build
pixi workspace channel add https://prefix.dev/robostack-jazzy
# Humble
pixi workspace channel add https://prefix.dev/robostack-humble --feature humble
pixi workspace environment add humble --feature humble
pixi add ros-humble-ros-base --feature humble
# Jazzy
pixi workspace channel add https://prefix.dev/robostack-jazzy --feature jazzy
pixi workspace environment add jazzy --feature jazzy
pixi add ros-jazzy-ros-base --feature jazzy
# Lint
pixi add pre-commit --feature lint
pixi workspace environment add lint --feature lint --no-default-feature
pixi task add lint "pre-commit run --all-files" --feature lint
```
