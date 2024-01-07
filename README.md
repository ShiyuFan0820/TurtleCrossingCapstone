# TurtleCrossingCapstone

**What will be made in the end:**  

<div align=center>
<img width="700" alt="image" src="https://github.com/ShiyuFan0820/PythonLearningNote/assets/149340606/a409f982-8873-453f-b9c0-2dd35c5f8f17">
</div>

[Python Daily Practice -- Turtle Crossing Capstone (Click here to watch the video)](https://youtu.be/enM9rD_ZgRo)

**The completed code of this game is in the [main_code.py](https://github.com/ShiyuFan0820/TurtleCrossingCapstone/blob/main/main_code.py) file.**

**Iusses Recorded: These are issues I encountered while writing this code, which may be helpful for you**

1. There was only one car even though I wrote the code to generate 100 cars.

_The code I wrote for the first time was (Just the relevant parts):_
```py
# Create the car class
COLORS = ["black", "purple", "green", "yellow", "red", "blue",
          "orange", "pink"]
CAR_COLOR = random.choice(COLORS)
Y_AXIS = random.randint(-240, 250)


class Car(Turtle):
    def __init__(self):
        super().__init__()
        self.shape("square")
        self.turtlesize(stretch_wid=1, stretch_len=2)
        self.color(CAR_COLOR)
        self.penup()
        self.goto(310, Y_AXIS)

    def move_car(self):
        self.backward(10)


# Create cars randomly
all_cars = []
for car_num in range(100):
    new_car = Car()
    all_cars.append(new_car)

is_game_on = True
while is_game_on:
    time.sleep(0.1)
    screen.update()
    for car in all_cars:
        car.move_car(random.randint(1, 10))

```
_There was only one car:_

<div align=center>
<img src="https://github.com/ShiyuFan0820/PythonLearningNote/assets/149340606/c9995407-5f55-4532-b637-44c5743ffaf8" width=370>
</div>

_Solution:_

The `CAR_COLOR` and `Y_AXIS` are outside the `Car` class, this means that all cars have the same color and same y cordination, resulting in all the cars overlap and look like there is only one car. To solve this problem the randomly choose shouldn't be put outside the class.

2. There is no gap between the cars, the turtle can't cross through the cars.

_After moving the `CAR_COLOR` and `Y_AXIS` inside the class, another issue occured, all cars moved at the same time, and there was no gap for the turtle to cross through._

<div align=center>
<img src="https://github.com/ShiyuFan0820/PythonLearningNote/assets/149340606/6e8a9a60-c375-4b54-9601-10c15c71a3b7" width=370>
</div>

_Solution:_

According to the above code, all generated cars are outside the while loop, they will move out at the same time and will not be generated again, the cars are supposed to be generated as long as the while loop runs and generated only every few time. I define a `car_circle` variable that can add by 1 every time the game loop, check whether it is divisible by 3 as a condition to create a new car, in this way the car would continue to be generated.
