# _init documentation

## Overview

This `__init__.py` file defines the public interface for a Python package related to risk assessment and hazard modeling. It imports and exposes various classes from different modules within the package.

## Imported Classes

### From `.assets` module:
1. `Asset`: Likely represents a general asset in the risk assessment context.
2. `PowerGeneratingAsset`: A specialized asset class, probably representing power plants or similar facilities.

### From `.curve` module:
3. `ExceedanceCurve`: Likely used for probability calculations in risk assessment.

### From `.hazard_event_distrib` module:
4. `HazardEventDistrib`: Probably represents the distribution of hazard events.

### From `.hazards` module:
5. `Hazard`: A base class for different types of hazards.
6. `Drought`: A specific type of hazard representing drought conditions.
7. `RiverineInundation`: Another specific hazard type, likely representing flooding from rivers.

### From `.vulnerability_distrib` module:
8. `VulnerabilityDistrib`: Likely represents the distribution of vulnerability for assets.

### From `.vulnerability_model` module:
9. `VulnerabilityModelAcuteBase`: Probably a base class for acute vulnerability models.

## Usage

When users import this package, they will have direct access to all these classes. For example:

```python
from your_package_name import Asset, PowerGeneratingAsset, ExceedanceCurve, Hazard, Drought

# Now you can use these classes directly
asset = Asset()
power_plant = PowerGeneratingAsset()
drought_hazard = Drought()
```

## Package Structure

This `__init__.py` file suggests that the package has at least the following structure:

```
your_package_name/
├── __init__.py
├── assets.py
├── curve.py
├── hazard_event_distrib.py
├── hazards.py
├── vulnerability_distrib.py
└── vulnerability_model.py
```

Each of these `.py` files contains the respective classes that are being imported in the `__init__.py` file.

## Notes for Developers

- When adding new modules or classes to the package, remember to update this `__init__.py` file to expose them at the package level if needed.
- Be cautious about circular imports. The current structure seems to avoid this, but it's something to keep in mind as the package grows.
- Consider adding type hints and docstrings to these classes in their respective modules to improve IDE support and documentation.

