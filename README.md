# 1. Discovery
curl -X GET http://localhost:8080/SmartCampusAPI/api/v1/

# 2. Create a Room
curl -X POST http://localhost:8080/SmartCampusAPI/api/v1/rooms \
  -H "Content-Type: application/json" \
  -d '{"id":"ENG-101","name":"Engineering Lab","capacity":30}'

# 3. Get all Rooms
curl -X GET http://localhost:8080/SmartCampusAPI/api/v1/rooms

# 4. Register a Sensor (valid roomId)
curl -X POST http://localhost:8080/SmartCampusAPI/api/v1/sensors \
  -H "Content-Type: application/json" \
  -d '{"id":"CO2-001","type":"CO2","status":"ACTIVE","currentValue":400,"roomId":"ENG-101"}'

# 5. Filter sensors by type
curl -X GET "http://localhost:8080/SmartCampusAPI/api/v1/sensors?type=CO2"

# 6. Post a reading
curl -X POST http://localhost:8080/SmartCampusAPI/api/v1/sensors/CO2-001/readings \
  -H "Content-Type: application/json" \
  -d '{"value":450.5}'

# 7. Try to delete a room with sensors (expect 409)
curl -X DELETE http://localhost:8080/SmartCampusAPI/api/v1/rooms/ENG-101

# 8. Register sensor with invalid roomId (expect 422)
curl -X POST http://localhost:8080/SmartCampusAPI/api/v1/sensors \
  -H "Content-Type: application/json" \
  -d '{"id":"TEMP-999","type":"Temperature","status":"ACTIVE","currentValue":0,"roomId":"FAKE-999"}'
