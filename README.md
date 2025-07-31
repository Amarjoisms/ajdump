# ajdump

APM
+----------------+         +----------------+         +-----------------+
|    Asset       |         |  Asset_Type    |         |   Location      |
+----------------+         +----------------+         +-----------------+
| asset_id (PK)  |         | type_id (PK)   |         | location_id (PK)|
| name           | <-----  | name           |         | name            |
| type_id (FK)   |         | description    |         | address         |
| location_id(FK)|                                  | city            |
| status         |                                     
| serial_number  |                                     
| purchase_date  |                                     
+----------------+                                     
        |                                            
        v                                            
+--------------------+         +------------------------+
|   Asset_User_Map   |         |   Maintenance_Log      |
+--------------------+         +------------------------+
| id (PK)            |         | log_id (PK)            |
| asset_id (FK)      |         | asset_id (FK)          |
| user_id (FK)       |         | log_date               |
| assigned_date      |         | description            |
| released_date      |         | performed_by (FK)      |
+--------------------+         +------------------------+
                                      |
                                      v
                             +----------------+
                             |     User       |
                             +----------------+
                             | user_id (PK)   |
                             | name           |
                             | email          |
                             | role           |
                             +----------------+

+------------------------+
|     Sensor_Data        | ← For "Trends", "Overview"
+------------------------+
| data_id (PK)           |
| asset_id (FK)          |
| timestamp              |
| temperature            |
| vibration              |
| power_status           |
| other_metrics          |
+------------------------+

+------------------------+         +---------------------------+
|      Alarm             |         |     Health_Index          | ← "Health Index"
+------------------------+         +---------------------------+
| alarm_id (PK)          |         | index_id (PK)             |
| asset_id (FK)          |         | asset_id (FK)             |
| timestamp              |         | calculated_on             |
| severity (Low/High)    |         | health_score              |
| message                |         | status (Good/Bad/Critical)|
| acknowledged (bool)    |         +---------------------------+
+------------------------+

+--------------------------+       +----------------------------+
|         FMEA             |       |       Dashboard_View       | ← Stores configs
+--------------------------+       +----------------------------+
| fmea_id (PK)             |       | view_id (PK)               |
| asset_id (FK)            |       | user_id (FK)               |
| failure_mode             |       | view_name                  |
| effect                   |       | filter_config (JSON)       |
| cause                    |       | chart_config (JSON)        |
| detection_method         |       +----------------------------+
| severity_score           |
| occurrence_score         |
| detection_score          |
| rpn (calculated)         |
+--------------------------+

+--------------------------+
|     Overview_Snapshot    | ← To record periodic summary
+--------------------------+
| snapshot_id (PK)         |
| asset_id (FK)            |
| timestamp                |
| status_summary           |
| latest_health_score      |
| active_alarms_count      |
| notes                    |
+--------------------------+
