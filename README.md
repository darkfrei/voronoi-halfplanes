# voronoi-halfplanes
Simple Voronoi halfplanes solution for LÖVE / Lua


# Voronoi Diagram Library for Lua / Love2D

This library provides a simple and flexible way to generate **Voronoi diagrams** in [Love2D](https://love2d.org/), a lightweight framework for making 2D games and visualizations. Using this library, you can create interactive Voronoi diagrams, add/remove sites dynamically, and customize the bounding polygon.

---

## What is a Voronoi Diagram?

A **Voronoi diagram** partitions a plane into regions based on the distance to a set of points (called "sites"). Each region corresponds to one site and contains all points closer to that site than to any other. Voronoi diagrams are widely used in computational geometry, game development, procedural generation, and data visualization.

![animation voronoi halfplanes](https://github.com/darkfrei/voronoi-halfplanes/blob/main/voronoi-halfplanes-02.gif)


---

## Voronoi Diagram Structure

1. Voronoi Diagram

- Fields:
  - `boundingPolygon`: The polygon defining the boundary of the diagram (default is a rectangle with vertices: 50, 50, 750, 50, 750, 550, 50, 550).
  - `sites`: A list of all sites (points) in the diagram.

  

  - `cells`: A list of Voronoi cells, each corresponding to a site.

  - `edges`: A list of all edges in the diagram.

  - `vertices`: A list of all vertices (intersection points of edges) in the diagram.


2. Site

Represents a single point in the Voronoi diagram.

- Fields:

  - `x`, `y`: Coordinates of the site.

  - `valid`: A boolean indicating whether the site lies within the bounding polygon.

  - `cell`: A reference to the Voronoi cell associated with this site.

3. Cell
   
- Fields:

  - `site`: A reference to the site associated with this cell.

  - `polygon`: A list of coordinates defining the cell's boundary polygon.

  - `vertices`: A list of vertices (corner points) of the cell.

  - `edges`: A list of edges forming the boundary of the cell.

  - `valid`: A boolean indicating whether the cell is valid (e.g., not clipped out by the bounding polygon).

4. Vertex
   
Represents a vertex (intersection point) in the Voronoi diagram.

- Fields:

  - `x`, `y`: Coordinates of the vertex.

  - `edges`: A list of edges connected to this vertex.

  - `cells`: A list of cells that share this vertex.

  - `id`: A unique identifier for the vertex.

5. Edge

Represents an edge (line segment) in the Voronoi diagram.

- Fields:

  - `v1`, `v2`: References to the two vertices that define the edge.

  - `cells`: A list of cells that share this edge (usually one or two cells).

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
4. Create a new Voronoi diagram object and start using the API.

## Usage
- **Basic Workflow** 
1. Create a New Diagram:
```lua
local diagram = Voronoi:newDiagram()
```

2. Set a Custom Bounding Polygon (Optional):
```lua
local customPolygon = {100, 100, 700, 100, 700, 500, 100, 500}
diagram:setBoundingPolygon(customPolygon)
```
3. Add Sites:
```lua
diagram:addSite(200, 200)
diagram:addSite(400, 300)
diagram:addSites({{x = 600, y = 250}, {x = 300, y = 400}})
```
4. Update Cells:
```lua
diagram:update()
```
5. Draw the Diagram:
```lua
function love.draw()
    -- Draw bounding polygon
    love.graphics.setColor(1, 1, 1, 0.2)
    diagram:drawBoundingPolygon('fill')
    love.graphics.setColor(1, 1, 1)
    diagram:drawBoundingPolygon('line')

    -- Draw Voronoi cells
    love.graphics.setColor(0, 1, 0, 0.3)
    diagram:drawCells('fill')
    love.graphics.setColor(0, 1, 0)
    diagram:drawCells('line')

    -- Draw sites
    love.graphics.setColor(1, 0, 0)
    diagram:drawSites('fill', 5)
end
```
6. Interactivity:
* Use `diagram:getCell(mx, my)` to detect which cell the mouse is over.
* Add or remove sites dynamically using mouse input.



## API Reference
## Core Methods

- `newDiagram()`: Creates a new Voronoi diagram object.
- `addSite(x, y)`: Adds a new site to the diagram.
- `addSites(sites)`: Adds multiple sites to the diagram.
- `removeSiteByIndex(index)`: Removes a site by its index.
- `removeLastSite()`: Removes the last added site.
  
- `setBoundingPolygon(polygon)`: Sets a custom bounding polygon for the diagram.
- `update()`: Generates Voronoi cells by clipping polygons for each site.

## Drawing Methods (Love2D)

Drawing methods: `drawBoundingPolygon`, `drawSites`, `drawCells`, `drawVertices`, etc.

## Utility Methods

Export method: `exportGraphToClipboard()` exports the graph in Lua format to the clipboard (vertices and edges).

## Example

![example voronoi halfplanes](https://github.com/darkfrei/voronoi-halfplanes/blob/main/voronoi-halfplanes-01.png)

This code demonstrates how to create and interact with a Voronoi diagram using the library. It includes adding and removing sites, modifying the bounding polygon, and highlighting cells under the mouse cursor.

```lua
-- main.lua

-- set the window title
love.window.setTitle('Voronoi lib halfplanes method')

-- require the Voronoi module
local Voronoi = require("Voronoi")

-- create a new Voronoi diagram object
local diagram = Voronoi:newDiagram()

-- initialize the diagram when the game starts
function love.load()
	-- define a custom bounding polygon
	local customPolygon = {150, 100, 750, 200, 700, 550, 100, 550}
	diagram:setBoundingPolygon(customPolygon)

	-- add sites to the diagram
	diagram:addSite(200, 200)
	diagram:addSite(400, 200)
	diagram:addSite(500, 200)
	diagram:addSite(600, 200)
	diagram:addSite(200, 400)
	diagram:addSite(300, 300)
	diagram:addSite(700, 300)
	diagram:addSite(400, 400)
	diagram:addSite(400, 500)
	diagram:addSite(500, 500)
	diagram:addSite(500, 400)
	diagram:addSite(600, 400)

	-- add a site outside the bounding polygon (for testing purposes)
	diagram:addSite(100, 200)

	-- update the diagram to generate Voronoi cells
	diagram:update()
end

-- handle mouse input
function love.mousepressed(mx, my, button)
	-- left mouse button adds a new site at the mouse position
	if button == 1 then
		diagram:addSite(mx, my)
		diagram:update()

		-- right mouse button removes a site
	elseif button == 2 then
		local index, cell = diagram:getCell(mx, my)
		if index then
			-- remove the site corresponding to the clicked cell
			diagram:removeSiteByIndex(index)
		else
			-- if no cell is clicked, remove the last site
			diagram:removeLastSite()
		end
		diagram:update()

		-- middle mouse button modifies the last vertex of the bounding polygon
	elseif button == 3 then
		local i = #diagram.boundingPolygon - 1
		diagram.boundingPolygon[i] = mx
		diagram.boundingPolygon[i + 1] = my

		-- update the diagram after modifying the bounding polygon
		diagram:update()
	end
end

-- draw the Voronoi diagram and interactive elements
function love.draw()
	-- draw the bounding polygon
	love.graphics.setColor(1, 1, 1, 0.2) -- semi-transparent white fill
	diagram:drawBoundingPolygon('fill')
	love.graphics.setColor(1, 1, 1) -- white outline
	diagram:drawBoundingPolygon('line')

	-- draw the Voronoi cells
	love.graphics.setColor(0, 1, 0, 0.3) -- green with transparency for cells
	diagram:drawCells('fill')
	love.graphics.setColor(0, 1, 0) -- green outline for cells
	diagram:drawCells('line')

	-- draw the sites
	love.graphics.setColor(0, 1, 0) -- green color for sites
	diagram:drawSites('fill', 5)

	-- highlight the cell under the mouse cursor
	local mx, my = love.mouse.getPosition()
	local index, cell = diagram:getCell(mx, my)
	if index then
		love.graphics.setColor(1, 1, 1, 0.6) -- semi-transparent white fill
		diagram:drawCell(index, 'fill')
		love.graphics.setColor(1, 1, 1, 1) -- solid white outline
		diagram:drawCell(index, 'line')

		love.graphics.setColor(1, 1, 1, 1) -- solid white circle for the site
		diagram:drawSite(index, 'fill', 5)
	end
end
```


