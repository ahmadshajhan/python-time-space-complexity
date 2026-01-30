# turtle Module

The `turtle` module provides a beginner-friendly graphics library based on Tk, allowing drawing with simple commands like moving a turtle.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| `forward()` / movement | O(1) | O(1) | Draw line segment; Tk rendering overhead |
| Draw shape | O(n) | O(n) | n = sides/segments |
| Screen refresh | O(n) | O(n) | Render all graphics objects |

## Drawing with Turtle Graphics

### Basic Turtle Drawing

```python
from turtle import Turtle, Screen

# Create screen and turtle - O(1)
screen = Screen()
turtle = Turtle()

# Draw square - O(n)
for _ in range(4):
    turtle.forward(100)  # O(1)
    turtle.right(90)      # O(1)

# Change properties - O(1)
turtle.pencolor("red")
turtle.pensize(3)

# Draw circle - O(n)
turtle.circle(50)

# Keep window open
screen.exitonclick()
```

### Multiple Turtles

```python
from turtle import Turtle, Screen

screen = Screen()

# Create turtles - O(1) each
turtle1 = Turtle()
turtle1.color("red")

turtle2 = Turtle()
turtle2.color("blue")
turtle2.penup()
turtle2.goto(-50, 0)
turtle2.pendown()

# Draw simultaneously - O(n)
for _ in range(100):
    turtle1.forward(1)
    turtle1.right(3.6)
    
    turtle2.forward(1)
    turtle2.left(3.6)

screen.exitonclick()
```

## Related Documentation

- [tkinter Module](tkinter.md)
