# Structing Machine Learning Projets

## Orthogonalization

It is necessary to tune the hypermeters systematically. It means we have to know which parameters to tune in ordre to achieve one effect. This process we call orthogonalization.

When we tune the parameters, it is well to assure that each parametres we tune just change the performence in one single aspects.

For example, firstly, we should find the best parameters will just have a influence in the training set.(Optimiser, for example)
And then we considre the model performence in dev set and test set.

We don't recommend to use early stop in the first step, because it will have effect in both training set and test set.

## Setting up your goal

### Single number evaluation metric

A single number evaluation will speed up the iterative process of imporving our machine learning alogrithm. If we have several numbers evaluation for metrics, we need to merge these numbers into a single number for picking a model more easily.

### Satisficing and Optimizing metric

If there are multiple things you care about, you can set one of them as the optimizing metric that you want to do as well as possible on and one or more as satisficing metrics were you'ill be satisfice.

### Train/dev/test distributions

The dev set and test set have to come from the same distribution. **This video just give the guideline, but don't give any approche to do it**
We can take this randomly shuffled data into the dev and test set.

### Size of the dev and test sets

If the dataset is small, we can apply the rule of thumbe of taking all the data you have and using a 70/30 split into a train and test set.

If the dataset is big enough, it might be quite reasonable to set up your data so that you have 98% in the training set, and 1% dev set, and 1% test set.

The test set is not necessary. But we don't recommand not having a test set when buinding a system. Because with test set, we reassuring to get an unbiased estimate. But if we have a dev set big enough, we can igonre the test set.

### When to change dev/test sets and metrics

Firstly we need to set the metric and dev set for driving the speed of our team iterating. If we find out the metric or the dev set are not good enough, we can change them at that time.

## Comparing to human-level performance

Raison:

- Because of advances in deep learning, machine learning algorithms are suddenly working much better and so ti has become competitive with human-level performance
- It turns out that the workflow of designing andbuilding a machine learning system, the workflow is much more efficient when you're trying to do something that humans can also do.

So in thoses settings, it becomes natural to take about comparing, or trying to mimic human-level performance.

Humans are quite good at a lot of tasks. So long as ML is worse than humansn you can:

- Get labeled data from humans
- Gain insight from manual error analysis:
  Why did a person get this right?
- Better analysis of bias/variance
