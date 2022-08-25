# Car Economy Predictions

## Get the data
```
curl http://archive.ics.uci.edu/ml/machine-learning-databases/auto-mpg/auto-mpg.data > auto-mpg.data

```
Use the `convert.ipynb` notebook to convert the data to CSV

## Train the model

```
ludwig experiment --dataset auto_mpg.csv   --config config.yaml

```

## Hyperparameter optimisation
```
ludwig hyperopt --dataset auto_mpg.csv   --config config.yaml
```

```
parent_path=/Users/chris.hunt/Dev/personal/tools/ludwigCarEfficiency

docker run -v ${parent_path}:/src  \
    ludwigai/ludwig:master \
    ludwig hyperopt --dataset auto_mpg.csv \
        --config /src/config.yaml \
        --output_directory /src/results

```

## Visualise the training data

```
ludwig visualize -v learning_curves \
-trs results/experiment_run/training_statistics.json
```

## Predict
### DMC DeLorean data

```
Cylinders,Displacement,Horsepower,Weight,Acceleration,ModelYear,Origin
6,174,130,2712,10.5,81,1
```

```
ludwig predict -m ./results/experiment_run/model/ --dataset predict.csv
```

Actual fuel economy: 22.8 mpg (conbined)
Source: https://www.telegraph.co.uk/cars/classic/back-to-the-future-day-is-the-delorean-as-bad-as-we-think/