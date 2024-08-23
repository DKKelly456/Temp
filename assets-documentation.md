# Assets Module Documentation

## Overview

This module defines various asset classes used in a risk assessment or asset management system, with a particular focus on power generating assets. It includes enumerations for fuel types, cooling systems, and turbine types, as well as classes for different types of assets.

## Enumerations

### `FuelKind` (Enum)
Represents different types of fuel used in power plants, based on the Global Power Plant Database v1.3.0.

Values include: Biomass, Coal, Cogeneration, Gas, Geothermal, Hydro, Nuclear, Oil, Other, Petcoke, Solar, Storage, Waste, WaveAndTidal, Wind

### `CoolingKind` (Enum)
Represents different cooling systems used in power plants.

Values:
- `Dry`: Affected by Air Temperature, Inundation
- `OnceThrough`: Affected by Drought, Inundation, Water Temperature, Water Stress
- `Recirculating`: Affected by Drought, Inundation, Water Temperature, Water Stress, Wet-Bulb Temperature

### `TurbineKind` (Enum)
Represents types of turbines used in power plants.

Values: Gas, Steam

## Classes

### `Asset`
Base class for all assets.

Attributes:
- `latitude` (float): Geographical latitude of the asset
- `longitude` (float): Geographical longitude of the asset
- `id` (Optional[str]): Unique identifier for the asset

### `WindTurbine` (dataclass)
Represents a wind turbine, inheriting from `Asset`.

Additional attributes:
- `capacity` (Optional[float]): Power generation capacity
- `hub_height` (Optional[float]): Height of the turbine hub
- `cut_in_speed` (Optional[float]): Minimum wind speed for operation
- `cut_out_speed` (Optional[float]): Maximum wind speed for operation
- `fixed_base` (Optional[bool]): Whether the turbine has a fixed base (default: True)
- `rotor_diameter` (Optional[float]): Diameter of the rotor

### `PowerGeneratingAsset`
Represents a generic power generating asset, inheriting from `Asset`.

Additional attributes:
- `type` (Optional[str]): Type of the power generating asset
- `location` (Optional[str]): Location of the asset
- `capacity` (Optional[float]): Power generation capacity
- `primary_fuel` (Optional[FuelKind]): Primary fuel used by the asset

### `ThermalPowerGeneratingAsset`
Represents a thermal power generating asset, inheriting from `PowerGeneratingAsset`.

Additional attributes:
- `turbine` (Optional[TurbineKind]): Type of turbine used
- `cooling` (Optional[CoolingKind]): Type of cooling system used

Methods:
- `get_inundation_protection_return_period()`: Returns the design return period for inundation protection (250 years for most plants, 10,000 years for nuclear plants)

### `RealEstateAsset`
Represents a real estate asset, inheriting from `Asset`.

Additional attributes:
- `location` (str): Location of the real estate
- `type` (str): Type of real estate

### `ManufacturingAsset`
Represents a manufacturing asset, inheriting from `Asset`.

Additional attributes:
- `location` (Optional[str]): Location of the manufacturing asset
- `type` (Optional[str]): Type of manufacturing asset

### `IndustrialActivity`
Represents an industrial activity, inheriting from `Asset`.

Additional attributes:
- `location` (Optional[str]): Location of the industrial activity
- `type` (str): Type of industrial activity

### `TestAsset`
A simple test asset class, inheriting from `Asset` with no additional attributes or methods.

## Usage Notes

1. The `Asset` class serves as the base for all other asset types, providing common attributes like latitude, longitude, and ID.

2. The `PowerGeneratingAsset` class uses a type string to determine the primary fuel. The type string can contain multiple archetypes separated by "/".

3. The `ThermalPowerGeneratingAsset` class extends this concept, using additional archetypes in the type string to determine turbine and cooling types.

4. The `get_inundation_protection_return_period()` method in `ThermalPowerGeneratingAsset` provides different protection levels for nuclear vs. non-nuclear plants.

5. Various asset types (RealEstate, Manufacturing, IndustrialActivity) are provided for different use cases in the risk assessment or asset management system.

6. The `TestAsset` class can be used for testing purposes or as a placeholder for future asset types.

