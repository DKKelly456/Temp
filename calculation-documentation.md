# Calculation Module Documentation

## Overview

This module serves as a configuration hub for the physical risk assessment system. It defines default hazard models, vulnerability models, and risk measure calculators for various asset types. The module also includes a factory class for creating risk measure calculators based on specific use cases.

## Imports

The module imports various components from the `physrisk` package, including hazard models, vulnerability models, and risk calculators. It also imports asset types from a local `.assets` module.

## Functions

### `get_default_hazard_model() -> HazardModel`

Returns the default hazard model, which is a `ZarrHazardModel` that retrieves hazard event data from Zarr storage.

### `get_default_vulnerability_models() -> Dict[type, Sequence[VulnerabilityModelBase]]`

Returns a dictionary mapping asset types to sequences of vulnerability models. This function defines the default vulnerability models for different asset types:

- `Asset`: Generic asset models (placeholder for unknown assets)
- `PowerGeneratingAsset`: Inundation model
- `RealEstateAsset`: Models for coastal and riverine inundation, tropical cyclones, and cooling
- `IndustrialActivity`: Chronic heat model
- `ThermalPowerGeneratingAsset`: Models for various thermal power plant vulnerabilities
- `TestAsset`: Temperature model

### `get_default_risk_measure_calculators() -> Dict[Type[Asset], RiskMeasureCalculator]`

Returns a dictionary mapping asset types to risk measure calculators. Currently, it only defines a calculator for `RealEstateAsset`.

## Classes

### `DefaultMeasuresFactory(RiskMeasuresFactory)`

A factory class for creating risk measure calculators based on specific use cases.

Methods:
- `calculators(self, use_case_id: str) -> Dict[Type[Asset], RiskMeasureCalculator]`:
  - If `use_case_id` is "generic", returns a dictionary with a `GenericScoreBasedRiskMeasures` calculator for the `Asset` type.
  - Otherwise, returns the result of `get_default_risk_measure_calculators()`.

## Key Components

1. **Hazard Model**: The default hazard model uses Zarr storage for retrieving hazard event data.

2. **Vulnerability Models**: 
   - For generic assets, placeholder models are used for various hazards (fire, chronic heat, hail, drought, precipitation).
   - Specific models are defined for power generating assets, real estate assets, industrial activities, and thermal power generating assets.
   - These models cover a range of hazards including inundation, tropical cyclones, chronic heat, and various thermal power plant-specific vulnerabilities.

3. **Risk Measure Calculators**: 
   - The default setup includes a specific calculator for real estate assets (`RealEstateToyRiskMeasures`).
   - The `DefaultMeasuresFactory` allows for dynamic selection of risk measure calculators based on the use case.

## Usage Notes

1. This module serves as a central configuration point for the physical risk assessment system. Users can modify these functions to customize the models and calculators used in their assessments.

2. The `get_default_vulnerability_models()` function allows for easy extension to support new asset types or vulnerability models.

3. The `DefaultMeasuresFactory` class provides a flexible way to select risk measure calculators based on different use cases. Users can extend this class to support additional use cases.

4. When adding new asset types or models, ensure they are imported correctly and added to the appropriate dictionaries in this module.

5. The use of placeholder vulnerability models (e.g., `PlaceholderVulnerabilityModel`) suggests that some parts of the system may still be under development or pending more specific implementations.

