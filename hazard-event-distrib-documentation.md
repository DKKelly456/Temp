# HazardEventDistrib Class Documentation

## Overview

The `HazardEventDistrib` class represents the intensity distribution of a hazard event (such as inundation depth or wind speed) specific to the location of an asset. It provides methods to manage and analyze the probability distribution of hazard intensities.

## Class Definition

```python
class HazardEventDistrib:
    __slots__ = ["__event_type", "__intensity_bins", "__prob", "__path", "__exceedance"]
```

The use of `__slots__` optimizes memory usage and provides faster attribute access.

## Constructor

```python
def __init__(
    self,
    event_type: type,
    intensity_bins: Union[List[float], np.ndarray],
    prob: Union[List[float], np.ndarray],
    path: List[str]
):
```

### Parameters:

- `event_type` (type): The type of hazard event.
- `intensity_bins` (Union[List[float], np.ndarray]): Non-decreasing intensity bin edges.
- `prob` (Union[List[float], np.ndarray]): Annual probability of occurrence for each intensity bin.
- `path` (List[str]): Path to the hazard indicator data source.

### Behavior:

- Initializes the class attributes with the provided values.
- Converts `intensity_bins` and `prob` to numpy arrays for efficient computation.

## Properties

### `intensity_bin_edges`

```python
@property
def intensity_bin_edges(self) -> np.ndarray:
```

Returns the array of intensity bin edges.

### `prob`

```python
@property
def prob(self) -> np.ndarray:
```

Returns the array of probabilities for each intensity bin.

### `path`

```python
@property
def path(self) -> List[str]:
```

Returns the path to the hazard indicator data source.

## Methods

### `intensity_bins()`

```python
def intensity_bins(self):
```

Returns a generator of tuples representing the lower and upper bounds of each intensity bin.

### `to_exceedance_curve()`

```python
def to_exceedance_curve(self):
```

Converts the probability distribution to an exceedance curve using the `curve.to_exceedance_curve()` function.

## Usage Example

```python
# Create a HazardEventDistrib instance
hazard_dist = HazardEventDistrib(
    event_type=WindEvent,
    intensity_bins=[0, 10, 20, 30, 40],
    prob=[0.5, 0.3, 0.15, 0.05],
    path=["wind_data", "location_123"]
)

# Access properties
print(hazard_dist.intensity_bin_edges)  # [0, 10, 20, 30, 40]
print(hazard_dist.prob)  # [0.5, 0.3, 0.15, 0.05]

# Iterate over intensity bins
for lower, upper in hazard_dist.intensity_bins():
    print(f"Bin: {lower} to {upper}")

# Convert to exceedance curve
exceedance_curve = hazard_dist.to_exceedance_curve()
```

## Notes

1. The class uses double underscore name mangling for its attributes, indicating that they are intended to be private.

2. The `intensity_bins` method returns a generator, which is memory-efficient for large datasets.

3. The `to_exceedance_curve()` method relies on an external `curve` module, which should be imported and available.

4. The class is designed to work with numpy arrays for efficient numerical operations.

5. The use of `Union[List[float], np.ndarray]` in the constructor allows for flexibility in input types.

## Potential Improvements

1. Add input validation in the constructor to ensure `intensity_bins` and `prob` have compatible shapes.

2. Implement additional methods for statistical analysis of the hazard distribution.

3. Add documentation strings (docstrings) to methods for better inline documentation.

4. Consider adding a method to visualize the probability distribution or exceedance curve.

5. Implement serialization methods if persistence of these objects is required.

