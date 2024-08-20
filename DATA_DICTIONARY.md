# Airport Airspace Sample Datasets - Data Dictionary
## Table of Contents:
- [Imaginary Surfaces for Civil Airports](#dataset-imaginary-surfaces-for-civil-airports)
- [Published Instrument Approach Procedures for Civil Airports](#dataset-published-instrument-approach-procedures-for-civil-airports)

## Dataset: Imaginary Surfaces for Civil Airports
**Filename:** imaginary_surfaces_rootgeo_sample.geojson

**Coordinate Reference System:** EPSG:4326 (World Geodetic System 1984)

**Description:**\
This dataset represents civil airport imaginary surfaces, as described in FAR 77.17(a)(2) and FAR 77.19. More specifically, it includes obstruction standard surfaces (as specified in FAR 77.17(a)(2)) and horizontal surfaces, conical surfaces, primary surfaces, approach surfaces, and transitional surfaces for precision runways (as specified in FAR 77.19). An object would be an obstruction to air navigation if it were tall enough to pierce, or intersect, any of these imaginary surfaces, at the location at which it was installed.

Many of the imaginary surfaces have complex 3D geometries (e.g., conical or sloping shapes); therefore, each imaginary surface in the dataset is represented as a 3D polygon in GIS format. The z-values of the vertices of the 3D polygons capture the elevation at each vertex in meters above mean sea level and, with proper 3D GIS visualization software, enable visualization of the surfaces in 3D.

For simpler 2D visualization and analysis, the attribute table also includes a summary of the range of elevation spanned by each imaginary surface, including the minimum and maximum elevation of each polygon in height above mean sea level (AMSL). The associated airport, and (if applicable) the associated runway identifier, are also provided.

**Attributes:**
- *feature* (string): Type of imaginary surface. Valid options include:
    - horizontal_surface: Horizontal surface for the airport (see FAR 77.19(a))
    - conical_surface: Conical surface for the airport (see FAR 77.19(b))
    - primary_surface: Primary surface for a runway (see FAR 77.19(c))
    - base_approach_surface: Approach surface for the “base” end of a runway with a visual or non-precision instrument approach (see FAR 77.19(d)).
    - recip_approach_surface: Same as previous but for the “reciprocal” end of a runway.
    - base_prec_approach_surface: Approach surface for the “base” end of a runway with a precision instrument approach (see FAR 77.19(d)).
    - recip_prec_approach_surface: Same as previous but for the “reciprocal” end of a runway.
    - base_prec_transition_surface: Transition surface for the “base” end of a runway with a precision instrument approach. Applies only to the section of the precision approach surface which projects through and beyond the limits of the conical surface (see FAR 77.19(e)).
    - recip_prec_transition_surface: Same as previous but for the “reciprocal” end of a runway.
    - inner_17a2_surface: Constant height obstruction standard surface within 3 nautical miles of the established reference point of an airport (see FAR 77.17(a)(2)).
    - outer_17a2_surface: Sloping obstruction standard surface extending outwards from the inner_17a2_surface (see FAR 77.17(a)(2)).
- *arpt_id* (string): Identifier for the airport associated with each imaginary surface
- *rwy_id* (string): Identifier for the runway associated with each imaginary surface, if applicable. Note that some imaginary surfaces are associated with the airport, rather than a specific runway. For these features (e.g., horizontal surface, conical surface, inner and outer 17(a)(2)), the rwy_id will be null.
- *elev_min_m* (float): Minimum elevation of the imaginary surface, in meters above mean sea level.
- *elev_max_m* (float): Maximum elevation of the imaginary surface, in meters above mean sea level. For non-sloping imaginary surfaces (e.g., primary surface, horizontal surface, inner_17a2_surface), this value will be the same as the elev_min_m.
- *elev_min_ft* (float): Minimum elevation of the imaginary surface, in feet above mean sea level.
- *elev_max_ft* (float): Maximum elevation of the imaginary surface, in feet above mean sea level. For non-sloping imaginary surfaces (e.g., primary surface, horizontal surface, inner_17a2_surface), this value will be the same as the elev_min_ft.


## Dataset: Published Instrument Approach Procedures for Civil Airports
**Filename:** instrument_approaches_rootgeo_sample.geojson

**Coordinate Reference System:** EPSG:4326 (World Geodetic System 1984)

**Description:**\
Instrument Approach Procedures represent sequences of flight maneuvers aircrafts may use to approach and land at an airport. These procedures provide clearance from known obstacles and apply when aircraft are flying under instrument flight rules (rather than visual flight rules).

Each feature in the instrument approach procedures dataset represents the approximate centerline of a single leg (i.e., segment or maneuver) of an approach procedure as a 3D line. The z-values of the line are typically based on the starting and ending altitudes of each segment and assume a constant descent or climb gradient. Z-values are in units of feet above mean sea level. Each line is also attributed with the starting and ending altitudes, in feet above mean sea level, as well as various identifiers as described in the Attributes section, below.

**Attributes:**
- *i* (integer): Identifier for the leg, starting with 0 at the first leg. Counting restarts for each procedure.
- *leg_type* (string): Path and termination type of each leg
- *start_fix* (string): Name/identifier of the fix from which the leg starts. If the leg does not start at a fix, this value will be null.
- *end_fix* (string): Name/identifier of the fix at which the leg ends. If the leg does not end at a fix, this value will be null.
- *start_altitude* (float): Starting altitude for the leg (altitude at the first vertex) in feet above mean sea level.
- *end_altitude* (float): Ending altitude for the leg (altitude at the last vertex) in feet above mean sea level.
- *missed_approach* (bool): Boolean flag indicating whether the leg is part of a missed approach procedure. Will be true if so and false otherwise.
- *procedure_id* (string): Identifier for the procedure to which the leg belongs. Procedures can be uniquely identified by combining this attribute with the airport_id column.
- *airport_id* (string): Identifier for the airport to which the procedure belongs.
