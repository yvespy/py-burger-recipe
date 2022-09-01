# Burger Recipe

**Please note:** read [the guideline](https://github.com/mate-academy/py-task-guideline/blob/main/README.md)
before starting.

You work at the In-N-Out and make delicious burgers. 

Create the `BurgerRecipe` class, its constructor should take and save the number of ingredients needed to make a burger, such as cheese, tomatoes, cutlets, eggs, buns, and sauce.

```python
cheese_burger = Burger(chesse=2, tomatoes=1, cutlets=1, eggs=1, buns=2, sauce="ketchup")
```

But, because the number of ingredients should be a whole number and it can range, it would be convenient to use descriptors here.

So, the quantity can range:
- `cheese` - from 0 to 2;
- `tomatoes` - from 0 to 3;
- `cutlets` - from 1 to 3;
- `eggs` - from 0 to 2;
- `buns` - from 2 to 3;
- `sauce` - can be ketchup, mayo, or burger.

Your task is to create the `Validator` descriptor, which should be an abstract class with methods:

- the `__set_name__` method, which takes the name of the attribute, adds `_` to its beginning and stores it in the `protected_name` attribute;
- the `__get__` method that returns the attribute value;
- the `__set__` method, which sets the attribute value (**note:** there should be no validation implemented);
- the `validate` abstract method which takes value.

Also, you need to implement the `Number` class, which is the `Validator` child class. It should have:

- the `__init__` method which takes and stores `min_value` and `max_value`;
- the `validate` method which should check the value type, and if the type is incorrect it must raise the `TypeError` exception with the message `Quantity should be integer`. 
Then it should check whether the value is within `min_value` and `max_value`, if it’s not it should raise the `ValueError` with the message `Quantity should not be less than {self.min_value} and greater than {self.max_value}.`

Last but not least, you need to implement the `OneOf` validator which is child class of the `Validator` and allows choosing one of the provided values and should have:
- the `__init__` method which takes and stores `options`;
- the `validate` method which takes `value` and checks if it’s one of the provided options and if not - raises the `ValueError` with the message `Expected {value} to be one of {self.options}.`

```python
burger = BurgerRecipe(cheese="1", tomatoes="1", cutlets="1", eggs="1", buns="1", sauce="mayo")
 # TypeError: Quantity should be integer.

burger = BurgerRecipe(cheese=10, tomatoes=1, cutlets=1, eggs=1, buns=1, sauce="mayo")
 # ValueError: Quantity should not be less than 0 and greater than 2.

burger = BurgerRecipe(cheese=1, tomatoes=1, cutlets=1, eggs=1, buns=2, sauce="mustard") 
# ValueError: Expected mustard to be one of ('ketchup', 'mayo', 'burger').

burger = BurgerRecipe(cheese=1, tomatoes=1, cutlets=1, eggs=1, buns=2, sauce="ketchup")
# burger will be created
```

**Please note:** descriptors should be created as class attributes.
