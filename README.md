## Refactoring

From the project on ISP19 named https://github.com/KasidisGit/riddle-me-this

In the riddle-me-this/model.py https://github.com/KasidisGit/riddle-me-this/blob/master/game/models.py
consider this code:

considering code..
```
class HardQuestion(models.Model):
    image = models.FileField(upload_to='img/hard', blank=False)
    answer = models.CharField(max_length=200)
    score = models.IntegerField(default=4)

    def __str__(self):
        return self.answer
```
```
class MediumQuestion(models.Model):
    image = models.FileField(upload_to='img/medium', blank=False)
    answer = models.CharField(max_length=200)
    score = models.IntegerField(default=3)

    def __str__(self):
        return self.answer
```
```
class EasyQuestion(models.Model):
    image = models.FileField(upload_to='img/easy', blank=False)
    answer = models.CharField(max_length=200)
    score = models.IntegerField(default=2)

    def __str__(self):
        return self.answer

```
* HardQuestion(), MediumQuestion() and EasyQuestion() have many the same variables. Extract superclass is the better choice and pull up field.

#### Extract Superclass:
  ```python
  class Role(models.Model):
      class Meta:
          abstract = True
  ```
  - First, we create a class.
#### Pull Up Field:
  ```python
  class Role(models.Model):
      answer = models.CharField(max_length=200)
      class Meta:
          abstract = True
  ```
  ```
  class HardQuestion(Role):
    image = models.FileField(upload_to='img/hard', blank=False)
    score = models.IntegerField(default=4)

    def __str__(self):
        return self.answer
  ```
  ```
  class MediumQuestion(Role):
    image = models.FileField(upload_to='img/medium', blank=False)
    score = models.IntegerField(default=3)

    def __str__(self):
        return self.answer
  ```
  ```
  class EasyQuestion(Role):
    image = models.FileField(upload_to='img/easy', blank=False)
    score = models.IntegerField(default=2)

    def __str__(self):
        return self.answer

  ```
  - Delete the same field in 3 classes and add those field into superclass 
