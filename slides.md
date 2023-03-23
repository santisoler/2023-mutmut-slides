<!-- .slide: class="center" -->

# Mutation testing with `mutmut`

## Testing your tests

---

<!-- .slide: class="center" -->

## Recap: testing our code

---

<!-- .slide: class="center" -->

## Test coverage

"The percentage of code that is executed <br>
 while running the full test suite."

---

<!-- .slide: class="center" -->

## What 100% coverage means?

100% coverage <strong style="color: #c44500">doesn't mean</strong> high quality tests

---

<!-- .slide: class="center" -->

### Example

```python
def f(x):
    return x ** 2


def test_f():
    assert f(1) == 1
```

---

<!-- .slide: class="center" -->

### Example: make it better

```python
import numpy as np

def f(x):
    return x ** 2

def test_f():
    values = np.array([1, 2, 5, -2, 0])
    expected = np.array([1, 4, 25, 4, 0])
    np.testing.assert_allclose(f(values), expected)
```

---

<!-- .slide: class="center" -->

## Goodhart's law

> "Any observed statistical regularity will tend to collapse <br>
> once pressure is placed upon it for control purposes"

or

> "When a metric becomes a goal, it stops being a metric"

---

<!-- .slide: class="center" -->

# Mutation testing

1. Apply a single mutation to our code
2. Run all tests
4. If all <strong class="green">tests pass</strong>:
   mark the **mutant** as <strong class="green">survived</strong>
3. If any of them <strong class="red">failed</strong>:
   mark that **mutant** as <strong class="red">killed</strong>
4. Restore the original code and go to step 1

---

<!-- .slide: class="center" -->

# `mutmut`: Python mutation tester

https://mutmut.readthedocs.io/en/latest/

---

<!-- .slide: class="center" -->

## Live coding!

---

<!-- .slide: class="center" -->

## Recommendations

- <strong class="organge">Backup yourself</strong>
    - Mutation are **destructive**
    - Use ``git`` (and have a backup)
- Mutation tests can take long time
    - Whitelist code
    - Don't run every mutation
    - Run `pytest` with `-x` option: _fail fast_
    - Be careful about running in CI
- `mutmut` is still buggy <span style="color: #aaa">(personal experience)</span>
    - See [Issue #259](https://github.com/boxed/mutmut/issues/259)

---

<!-- .slide: class="center" -->

## Alternatives

- [Cosmic Ray](https://cosmic-ray.readthedocs.io/en/latest/)
- [MutPy](https://github.com/mutpy/mutpy)
