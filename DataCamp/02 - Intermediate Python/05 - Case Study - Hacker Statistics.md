# Intermediate Python

## Case Study: Hacker Statistics

### Random Numbers

You need to import numpy, and inside numpy, there is the random package. Inside that package we find the "rand" function.

```python
import numpy as np
np.random.rand() # Pseudo-random number
```

### Random Walk

We build a for loop that should run ten times.
We can do this with the range() function, that generates a list of numbers that you can use to iterate over.

```python
import numpy as np
np.random.seed(123)
outcomes = []
for x in range(10) :
  coin = np.random.randint(0, 2)
  if coin == 0 :
    outcomes.append("head")
  else :
    outcomes.append("tails")
print(outcomes)
```

## Types of functions -

1. `np.random.rand()` -

   1. Computers typically generate so-called pseudo-random numbers.
   2. Those are random numbers that are generated using a mathematical formula, starting from a random seed.
   3. This seed was chosen by python when we called the rand function, but you can also set this manually.
   4. E.g -

   ```python
    import numpy as np
    np.random.rand() # Pseudo-random number
    ###################
    np.random.seed(123) # Starting from a seed
    np.random.rand() # Same seed ensures same numbers
    # It ensures the "reproductivity" of the ans.
   ```

2. `np.random.randint()` -

   1. A
   2. B
   3. E.g -

   ```python
    import numpy as np
    np.random.seed(123)
    coin = np.random.randint(0,2) # Randomly generates 0 or 1
   ```

3. `np.array()` -

   1. Converts an array to a numpy array.
   2. E.g - `np.array(all_walks)`.

4. `np.transpose()` -
   1. We can transpose a numpy array with it.
   2. E.g - `np.transpose(np_aw)`
