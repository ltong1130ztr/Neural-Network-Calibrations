## Neural Network Calibration Gist
This repo contains the following calibration methods for deep neural networks:
- temperature scaling
- class-wise temperature scaling
- histogram binning [[1](#1)]

## Setup
- python 3.x
- pytorch>=1.8
- matplotlib
- numpy

## Histogram Binning
The histogram binning [[1](#1)] approach is implemented within the class `histogram_binning_calibration`. Further more, a linear rescaling of the remaining
softmax scores according to the calibrated argmax-selected softmax score is also
implemented.

#### Example
```python
# load base model
base_model = load_model(model_path)
device = 'cuda'

# initialize class instance
n_bins = 15 # number of bins in the histogram
hist_est = histogram_binning_calibration(base_model,n_bins,device)

# setup validation set data loader here

# learn histogram from validation examples
hist_est.histogram_binning(val_loader)

# setup test set data loader here

# apply histogram binning on test data
sm_calib, flags, preds = hist_est(test_data)
```









## Reference
[[1](#1)] Zadrozny, Bianca and Elkan, Charles. Obtaining calibrated probability estimates from decision trees and naive bayesian classifiers. In ICML, pp. 609–616, 2001.