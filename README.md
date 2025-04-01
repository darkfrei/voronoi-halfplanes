# voronoi-halfplanes
Simple Voronoi halfplanes solution for LÖVE / Lua


# Voronoi Diagram Library for Love2D

This library provides a simple and flexible way to generate **Voronoi diagrams** in [Love2D](https://love2d.org/), a lightweight framework for making 2D games and visualizations. Using this library, you can create interactive Voronoi diagrams, add/remove sites dynamically, and customize the bounding polygon.

---

## What is a Voronoi Diagram?

A **Voronoi diagram** partitions a plane into regions based on the distance to a set of points (called "sites"). Each region corresponds to one site and contains all points closer to that site than to any other. Voronoi diagrams are widely used in computational geometry, game development, procedural generation, and data visualization.

---

## Features

- **Dynamic Site Management**: Add or remove sites interactively.
- **Custom Bounding Polygon**: Define your own bounding polygon for clipping Voronoi cells.
- **Interactive Highlighting**: Detect and highlight the cell under the mouse cursor.
- **Modular Design**: Easy-to-use API with methods for drawing, updating, and managing the diagram.
- **Love2D Integration**: Designed specifically for Love2D, making it easy to integrate into your projects.

---

## Installation

1. Download the `voronoi.lua` file from this repository.
2. Place the file in your project directory.
3. Require the module in your `main.lua` file:
   ```lua
   local Voronoi = require("Voronoi")
   ```

