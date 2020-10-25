## Refactoring

From my project on programming2 named Zego https://github.com/JirawadeeSampusri/Zego

In the Zego/main.py

https://github.com/JirawadeeSampusri/Zego/blob/master/main.py

consider this code:

```def update(self):
        self.center_x += self.change_x
        self.center_y += self.change_y

        if self.left < 0:
            self.left = 0
        elif self.right > SCREEN_WIDTH - 1:
            self.right = SCREEN_WIDTH - 1

        if self.bottom < 0:
            self.bottom = 0
        elif self.top > SCREEN_HEIGHT - 1:
            self.top = SCREEN_HEIGHT - 1
```

* Refactoring Signs: 
  - In this method have two functions that can be seperated into two methods that easier to modify later.

* Refactoring: extract method

```def update_x_axis(self):
        self.center_x += self.change_x
        if self.left < 0:
            self.left = 0
        elif self.right > SCREEN_WIDTH - 1:
            self.right = SCREEN_WIDTH - 1
```
```def update_y_axis(self):
        self.center_y += self.change_y
        if self.bottom < 0:
            self.bottom = 0
        elif self.top > SCREEN_HEIGHT - 1:
            self.top = SCREEN_HEIGHT - 1
```




  
