# Camera Database Project

## Overview
This repository contains a database of digital cameras with detailed specifications and technical information. The database includes information on about 3,835 camera models across 36 brands.

## Data Statistics
- **Total Camera Models:** 3,835
- **Camera Brands:** 36
- **Total lines of data:** 185169
- **Coverage:** Professional DSLRs, mirrorless cameras, compact cameras, and specialised equipment, plus much more.

## Repository Structure
    ```bash
    ├───JSON
    │       brands.json 
    │       camera_data.json # Primary data file with all camera information
    │       just_models.json # Just the camera models, in a JSON list
    │       models.json # The models but in a dictionary structure
    │
    │
    └───TXT
            brands.txt # TXT file of every manufacturer, with each on a new line
            models.txt # TXT file of every model, with each on a new line
    ```


## Available Data Formats

### JSON
- **camera_data.json** - Complete database with all camera specifications
- **brands.json** - List of all camera brands
- **models.json** - List of cameras grouped by brand (without specifications)
- **just_models.json** - Simple list of all camera model names

### Text
- **brands.txt** - One camera brand per line
- **models.txt** - One camera model per line

### SQLite Database
The data is also available as a SQLite database with the following schema:
- **brands** table - Information about camera manufacturers
- **cameras** table - Basic camera model information
- **specs** table - Detailed specifications for each camera

# Example SQLite Queries

### Find cameras with high megapixel counts:
```sql
SELECT b.name as brand, c.name as model, s.spec_value as megapixels
FROM cameras c
JOIN brands b ON c.brand_id = b.id
JOIN specs s ON c.id = s.camera_id
WHERE s.spec_name = 'effective megapixels' 
AND CAST(REPLACE(s.spec_value, '.', '') AS FLOAT) > 30
ORDER BY CAST(REPLACE(s.spec_value, '.', '') AS FLOAT) DESC;
```

### Count cameras by brand:
```sql
SELECT b.name, COUNT(*) as camera_count
FROM cameras c
JOIN brands b ON c.brand_id = b.id
GROUP BY b.name
ORDER BY camera_count DESC;
```

# Data Updates
I will update the data ever so often. If a camera is missing please open an issue and I'll fix it.