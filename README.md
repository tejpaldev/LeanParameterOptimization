# LeanOptimization
Parameter optimization for LEAN

This toolset allows you to execute multiple parallel backtests using a local Lean clone. It is possible to configure several different optimization methods to fit your trading algorithm to an array of different success measures. 

You must edit the config file [optimization.json](https://github.com/jameschch/LeanOptimization/blob/master/Optimization/optimization.json) to define parameters and other settings. The gene values are fed into the Lean config and can be accessed in an algorithm using the QuantConnect.Configuration.Config methods.

An example algorithm is provided here: [ParameterizedAlgorithm](https://github.com/jameschch/LeanOptimization/blob/master/Optimization.Example/ParameterizedAlgorithm.cs)

## Quickstart
1. Clone local Lean.
2. Clone the Optimizer so that it shares the same parent folder as the Lean clone.
3. Edit the config file and enter the location of your trading algorithm dll in "algorithmLocation".
4. Now enter the class name of your algorithm in "algorithmTypeName".
5. Enter the location of your trade and quote bar data in the "dataFolder" setting.
6. Configure the maxThreads to define the number of parallel backtests.

## Configuration
Full documentation is provided in comments: [OptimizerConfiguration](https://github.com/jameschch/LeanOptimization/blob/master/Optimization/OptimizerConfiguration.cs)

The most important options:

### fitnessTypeName

#### Genetic
The default OptimizerFitness is a simple Sharpe Ratio tournament. There is also CompoundingAnnualReturnFitness to maximize raw returns. It is possible to optimize any Lean statistic using ConfiguredFitness.

#### SharpeMaximizer
Specifying the SharpeMaximizer fitness allows access to all of the optimization methods provided by the SharpLearning library. These include Random Search. Grid Search, Particle Swarm, Smac and several others.

#### Specialist Optimization
The simple SharpeMaximizer has been extended in NFoldCrossSharpeMaximizer so that the success score is measured over N-fold periods. This will prevent overfitting to a single in-sample period. 

Also now available is an experimental release of N-fold Walk Forward optimization (WalkForwardSharpeMaximizer).

## General

The optimizers support multiple parallel executions as standard. Currently, the following methods are available:
-Genetic Tournament
-Random Search
-Grid (exhaustive) Search
-Particle Swarm
-Bayesian
-Globalized Bounded Nelder Mead

These methods can target several fitness and maximization goals:
-N-Fold Cross-Validated Sharpe Ratio
-N-Fold Cross-Validated Compounding Annual Return
-Nested Cross-Validated Sharpe Ratio
-Walk Forward Period Optimized Sharpe Ratio
-Any Lean algorithm statistic (Sharpe Ratio, Alpha, Win Rate, etc)

If it possible to run each parallel backtest in an isolated AppDomain, or in a single AppDomain. The latter option can be useful for training a machine learning model.

## Interfaces (WIP)

Now also provided are several Blazor interfaces:

-Optimization Config Editor
-Optimization Results Charting
-Algorithm Code Editor (C#, Javascript)

## WIP

-Currently supporting in-browser multi-threaded optimization (i.e. running server-less) of basic algorithms
-Python running in browser
-User supplied C# to wasm compile in browser
-Genetic optimization in browser

