# automl-fall-school-2022

[AutoML Fall School 2022](https://sites.google.com/view/automl-fall-school-2022/): H2O AutoML Hands-on Workshop

📅 October 10, 2022

🇩🇪 Freiburg, Germany (and remote)


# H2O AutoML Tutorial in Python

AutoML is a function in H2O that automates the process of building a large number of models, with the goal of finding the "best" model without any prior knowledge or effort by the Data Scientist.  

H2O AutoML can be used for automating the machine learning workflow, which includes automatic training and tuning of many models within a user-specified time-limit. H2O offers a number of [model explainability methods](http://docs.h2o.ai/h2o/latest-stable/h2o-docs/explain.html) that apply to AutoML objects (groups of models), as well as individual models (e.g. leader model). Explanations can be generated automatically with a single function call, providing a simple interface to exploring and explaining the AutoML models.

The current version of AutoML trains and cross-validates the following algorithms: three pre-specified XGBoost GBM (Gradient Boosting Machine) models, a fixed grid of GLMs, a default Random Forest (DRF), five pre-specified H2O GBMs, a near-default Deep Neural Net, an Extremely Randomized Forest (XRT), a random grid of XGBoost GBMs, a random grid of H2O GBMs, and a random grid of Deep Neural Nets. In some cases, there will not be enough time to complete all the algorithms, so some may be missing from the leaderboard. In other cases, the grids will stop early, and if there’s time left, the top two random grids will be restarted to train more models. AutoML trains multiple Stacked Ensemble models throughout the process.

AutoML trains several Stacked Ensemble models during the run (unless ensembles are turned off using `exclude_algos`). We have subdivided the model training in AutoML into “model groups” with different priority levels. After each group is completed, and at the very end of the AutoML process, we train (at most) two additional Stacked Ensembles with the existing models. There are currently two types of Stacked Ensembles: one which includes all the base models (“All Models”), and one comprised only of the best model from each algorithm family (“Best of Family”). The Best of Family ensembles are more optimized for production use since it only contains six (or fewer) base models. It should be relatively fast to use in production (to generate predictions on new data) without much degradation in model performance when compared to the final “All Models” ensemble, for example. This may be useful if you want the model performance boost from ensembling without the added time or complexity of a large ensemble. You can also inspect some of the earlier “All Models” Stacked Ensembles that have fewer models as an alternative to the Best of Family ensembles. The metalearner used in all ensembles is a variant of the default Stacked Ensemble metalearner: a non-negative GLM with regularization (Lasso or Elastic net, chosen by CV) to encourage more sparse ensembles. The metalearner also uses a logit transform (on the base learner CV preds) for classification tasks before training.


- More information and code examples are available in the [AutoML User Guide](http://docs.h2o.ai/h2o/latest-stable/h2o-docs/automl.html).

- New features and improvements planned for AutoML are listed [here](https://0xdata.atlassian.net/issues/?filter=21603) and all AutoML tickets (bugs, new features) are listed [here](https://h2oai.atlassian.net/issues/?filter=20700).


## Installation

This Jupyter notebook requires the **h2o** Python package, and a few others.  The notebook was created with h2o v3.38.0.1.  If you'd like to install the requirements in a virtual environment from scratch, here's how to do that using venv:

```
python3 -m venv ./venv
source venv/bin/activate
pip3 install -r requirements.txt
```

Or if you're using conda: `conda install -c h2oai h2o`

To start the notebook, simply type: `jupyter notebook` and it will open file browser in your browser and you can double click the `automl-fall-school-2022-h2o-automl.ipynb` file.

