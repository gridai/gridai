# Hyperparameter sweeps

## Hyperparameter Sweeps

Grid allows running hyperparameter sweeps without changing a single line of code! Just make sure your script can take arguments:

```bash
python main.py --layers 32 --learning_rate 0.01
```

## Python flags

### boolean

Passing in a flag without values is treated like a boolean

```text
grid run main.py --do_something
```

### float

Grid supports standard float notation and scientific notation

```text
grid run main.py --learning_rate 0.01
grid run main.py --learning_rate 1e-2
```

### int

Grid supports standard integer notation

```text
grid run main.py --batch_size 32
```

### string

Grid supports standard string notation

```text
grid run main.py --model bert
grid run main.py --model 'bert'
grid run main.py --model "bert"
```

## Grid extensions

### distribution

Calls the script with each value sampled from any [numpy distribution](https://numpy.org/doc/1.16/reference/routines.random.html#distributions).

```text
grid run main.py --alpha "uniform(1e-5, 1e-1, 3)"
```

Grid will submit 3 jobs here:

```bash
# job 1
grid run main.py --alpha 0.03977392,

# job 2
grid run main.py --alpha 0.04835479

# job 3
grid run main.py --alpha 0.05200016
```

This is equivalent to:

```bash
>>> np.random.uniform(1e-5, 1e-1, 3)
array([0.03977392, 0.04835479, 0.05200016])
```

### list

Calls the script with each value in the list

```text
grid run main.py --layers "[32, 64, 128]"
```

Grid will submit 3 jobs here:

```bash
# job 1
grid run main.py --layers 32

# job 2
grid run main.py --layers 64

# job 3
grid run main.py --layers 128
```

### range

Calls the script with each value in the range.

```text
grid run main.py --layers "(1, 10, 2)"
```

Grid will submit 3 jobs here:

```bash
# job 1
grid run main.py --layers 1

# job 2
grid run main.py --layers 3

# job 3
grid run main.py --layers 5

# job 4
grid run main.py --layers 7

# job 5
grid run main.py --layers 9
```

This is equivalent to the [Python Range syntax](https://www.w3schools.com/python/ref_func_range.asp)

```bash
>>> list(range(1, 10, 2))
[1, 3, 5, 7, 9]
```

### string list

Calls the script with each value in the list

```text
grid run main.py --model "['resnet18' 'transformer', 'resnet50']"
```

Grid will submit 3 jobs here:

```bash
# job 1
grid run main.py --model resnet18

# job 2
grid run main.py --model transformer

# job 3
grid run main.py --model resnet50
```

## Grid Search

To generate combinations \(ie: a Grid Search\), pass in multiple flags

```text
grid run main.py --alpha "uniform(1e-5, 1e-1, 3)" --beta "[1, 2, 3, 4]"
```

Generates 3 x 4 = 12 experiments

```bash
grid run main.py --alpha 0.03977392 --beta 1
grid run main.py --alpha 0.03977392 --beta 2
grid run main.py --alpha 0.03977392 --beta 3
grid run main.py --alpha 0.03977392 --beta 4

grid run main.py --alpha 0.04835479 --beta 1
grid run main.py --alpha 0.04835479 --beta 2
grid run main.py --alpha 0.04835479 --beta 3
grid run main.py --alpha 0.04835479 --beta 4

grid run main.py --alpha 0.05200016 --beta 1
grid run main.py --alpha 0.05200016 --beta 2
grid run main.py --alpha 0.05200016 --beta 3
grid run main.py --alpha 0.05200016 --beta 4
```

To run only a sample of these, choose the Random search option.

## Random Search

The following command, generates 12 experiments.

```text
grid run main.py --alpha "uniform(1e-5, 1e-1, 3)" --beta "[1, 2, 3, 4]"
```

Generates 3 x 4 = 12 experiments

```bash
grid run main.py --alpha 0.03977392 --beta 1
grid run main.py --alpha 0.03977392 --beta 2
grid run main.py --alpha 0.03977392 --beta 3
grid run main.py --alpha 0.03977392 --beta 4

grid run main.py --alpha 0.04835479 --beta 1
grid run main.py --alpha 0.04835479 --beta 2
grid run main.py --alpha 0.04835479 --beta 3
grid run main.py --alpha 0.04835479 --beta 4

grid run main.py --alpha 0.05200016 --beta 1
grid run main.py --alpha 0.05200016 --beta 2
grid run main.py --alpha 0.05200016 --beta 3
grid run main.py --alpha 0.05200016 --beta 4
```

Using [Random Search](https://jmlr.csail.mit.edu/papers/volume13/bergstra12a/bergstra12a.pdf) you can get close to optimal performance without needing to run all possible combinations. To use random search with Grid, simply choose that option

```text
grid run --strategy random_search \
         --trials 3 \
         main.py \
         --alpha "uniform(1e-5, 1e-1, 3)" \
         --beta "[1, 2, 3, 4]"
```

This will choose a subset of the combinations generated and only run 3 experiments.

```bash
grid run main.py --alpha 0.03977392 --beta 1
grid run main.py --alpha 0.03977392 --beta 2
grid run main.py --alpha 0.03977392 --beta 3 # <-- chosen (randomly)
grid run main.py --alpha 0.03977392 --beta 4

grid run main.py --alpha 0.04835479 --beta 1 # <-- chosen (randomly)
grid run main.py --alpha 0.04835479 --beta 2
grid run main.py --alpha 0.04835479 --beta 3 # <-- chosen (randomly)
grid run main.py --alpha 0.04835479 --beta 4

grid run main.py --alpha 0.05200016 --beta 1
grid run main.py --alpha 0.05200016 --beta 2
grid run main.py --alpha 0.05200016 --beta 3
grid run main.py --alpha 0.05200016 --beta 4
```

## Bayesian optimization

There are alternative algorithms to random search that attempt to search the space more efficiently.

In practice, random search is hard to beat with random search. In certain applications/models, bayesian can give you a slight advantage. However, these cases are rare.

