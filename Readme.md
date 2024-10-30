# Road Construction Data Import Tool

## Introduction
This Python-based tool imports and manages road construction data into a PostgreSQL/PostGIS database. It processes GeoJSON files containing road construction and roadworks data, supporting both Polygon and MultiPolygon geometries. The tool includes features for data insertion, spatial querying, and validation.

## Prerequisites
- Python 3.7+
- PostgreSQL 12+ with PostGIS extension
- psycopg2-binary
- GeoJSON data files for road construction

## Installation

1. Clone the repository:

```bash
git clone https://github.com/yourusername/road-construction-data-import.git
cd road-construction-data-import
```

2. Create a virtual environment:

```bash
python -m venv .venv

for mac/linux:
source .venv/bin/activate

for windows:
.venv\Scripts\activate
```

3. Install the required Python packages:

```bash
pip install -r requirements.txt
```

## How to run

1. Make sure to replace the connection string in the script with your own.

```
connection_string = ""
```

2. To run the road speed limit script
```bash
python insert_road.py
```

3. To run the roadworks script
```bash
python insert_roadworks.py
```



## Features

### Data Import
- Batch processing for efficient data insertion
- Support for both Polygon and MultiPolygon geometries
- Error handling and logging
- Transaction management with rollback capability

### Spatial Queries
- Find nearby construction sites
- Distance-based searches
- Geometry validation and conversion

### Database Schema
The road_construction table includes:
- Worksite identification (code, name)
- Project details
- Temporal information (start/end dates)
- Spatial data (PostGIS geometry)
- Status tracking
- Shape metrics

## Function Documentation

### insert_roadworks.py

#### `geometry_to_wkt(geometry)`
Converts GeoJSON geometry to WKT format.
- Input: GeoJSON geometry object
- Output: WKT string
- Supports: Polygon and MultiPolygon

#### `insert_road_construction_data(connection_string, geojson_file_path)`
Imports GeoJSON data into PostgreSQL.
- Processes data in batches
- Handles errors per feature
- Provides progress logging

#### `create_road_construction_table(connection_string)`
Sets up database table and PostGIS extension.
- Creates spatial indexes
- Configures geometry columns
- Establishes constraints

#### `test_insertion(connection_string, test_lat, test_lon)`
Validates imported data through spatial queries.
- Checks record count
- Tests spatial searches
- Verifies geometry storage

## Error Handling
- Batch processing with rollback support
- Detailed error logging
- Geometry validation
- Connection management
- Exception handling for data processing

## Best Practices
1. Always backup your database before large imports
2. Monitor system resources during batch processing
3. Adjust batch size based on available memory
4. Verify data integrity after import
5. Use appropriate coordinate systems (EPSG:4326)

## Troubleshooting

### Common Issues
1. Connection errors:
   - Verify database credentials
   - Check database server status
   - Confirm network connectivity

2. Import failures:
   - Validate GeoJSON format
   - Check memory availability
   - Review log files for errors

3. Spatial query issues:
   - Confirm PostGIS extension
   - Verify coordinate systems
   - Check geometry validity

## Contributing
1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## License

MIT License

Copyright (c) 2024

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.