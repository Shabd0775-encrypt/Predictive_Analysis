# Assignment 1

Roll Number: 102303756

This project applies a roll-number-based non-linear transformation on
the NO2 feature and estimates the parameters of the probability density
function:

p̂(z) = c \* exp(-λ (z - μ)\^2)

Steps performed: - Loaded NO2 data from the dataset - Computed ar and br
using the roll number - Applied the transformation z = x + ar \*
arcsin(br \* x) - Estimated μ, λ and c using statistical estimation
(MLE)

Requirements: - Python 3 - NumPy - Pandas
