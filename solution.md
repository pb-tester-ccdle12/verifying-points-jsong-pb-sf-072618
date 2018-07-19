
# Verifying Points on a Curve


```python
# Verify curve Example

prime = 137
x, y = 73, 128

print(y**2 % prime == (x**3 + 7) % prime)
```

### Try it

Find out which points are valid on the curve \\( y^2 = x^3 + 7: F_{223} \\)

```
(192,105), (17,56), (200,119), (1,193), (42,99)
```


```python
from ecc import FieldElement, Point

prime = 223
a = FieldElement(0, prime)
b = FieldElement(7, prime)

points = ((192,105), (17,56), (200,119), (1,193), (42,99))

# iterate over points
for x_raw, y_raw in points:
    # Initialize points this way:
    # x = FieldElement(x_raw, prime)
    # y = FieldElement(y_raw, prime)
    x = FieldElement(x_raw, prime)
    y = FieldElement(y_raw, prime)
    # try initializing, RuntimeError means not on curve
    # p = Point(x, y, a, b)
    try:
        p = Point(x, y, a, b)
        print('({},{}) is on the curve'.format(x_raw, y_raw))
    except RuntimeError:
        print('({},{}) is not on the curve'.format(x_raw, y_raw))
```

### Test Driven Exercise

It's your turn to write a test now. Write the test below checking for whether the point is on the curve using the comments as a guide.


```python
from helper import run_test
from unittest import TestCase
from ecc import FieldElement, Point

class ECCTest(TestCase):



    def test_on_curve(self):
        # tests the following points whether they are on the curve or not
        # on curve y^2=x^3-7 over F_223:
        # (192,105) (17,56) (200,119) (1,193) (42,99)
        # the ones that aren't should raise a RuntimeError
        prime = 223
        a = FieldElement(0, prime)
        b = FieldElement(7, prime)
        
        valid_points = ((192,105), (17,56), (1,193))
        invalid_points = ((200,119), (42,99))
        
        # iterate over valid points
        for x_raw, y_raw in valid_points:
            # Initialize points this way:
            # x = FieldElement(x_raw, prime)
            # y = FieldElement(y_raw, prime)
            # Point(x, y, a, b)
            x = FieldElement(x_raw, prime)
            y = FieldElement(y_raw, prime)
            # Creating the point should not result in an error
            Point(x, y, a, b)

        # iterate over invalid points
        for x_raw, y_raw in invalid_points:
            # Initialize points this way:
            # x = FieldElement(x_raw, prime)
            # y = FieldElement(y_raw, prime)
            # Point(x, y, a, b)
            x = FieldElement(x_raw, prime)
            y = FieldElement(y_raw, prime)
            # check that creating the point results in a RuntimeError
            # with self.assertRaises(RuntimeError):
            #     Point(x, y, a, b)
            with self.assertRaises(RuntimeError):
                Point(x, y, a, b)
```


```python
run_test(ECCTest('test_on_curve'))
```
