# Hotel Reservation System

> This is a summary of Chapter 7 of [System Design Interview Volume 2](https://www.amazon.com/System-Design-Interview-Insiders-Guide/dp/1736049119).

## 1. Gather Requirements

- Scale: 5K Hotels, 1M rooms
- How rooms are booked: on the web/app, pay for reservation in full
- Reservations cancelable? yes
- Overbooking allowed? 10%
- Clarify Scope:
  - Views: hotel, hotel room
  - Reservation with overbooking feature
    - Also: prices change daily
  - Admin panel

Non-functional requirements:
- high concurrency
- medium latency

### Back-of-the-envelope Estimation

Given 5K Hotels, 1M rooms, estimiated daily reservations:
- On average: assume 70% occupancy, 3 day reservation
- 1M * 0.7 / 3 = ~240K Reservations/day.
- 86,400 seconds in a day =~ 100K seconds.
- QPS = Reservations/second = 240,000/100,000 = ~3.
- Assume only 10% of the people move to the next step in reservations:
  - QPS Reservations = 3
  - QPS Bookings = 30
  - QPS Viewings = 300


## 2. Propose High-Level Design

### API design

**REST endpoints**
 - GET/PUT/DELETE /v1/entity/ID  
 - POST /v1/entity
 - Entities: hotel, reservation
 - Nested entities: room and roomType (i.e. /v1/hotels/ID/rooms/ID, /v1/hotels/ID/roomTypes/ID)

**JSON shape:**
```json
{
    "startDate": "2021-04-28",
    "endDate": "2021-04-30",
    "hotelId": "245",
    "roomTypeId": "12345",
    "reservationId": "134235"
}
``` 

reservationId is the `idempotency` key to prevent double booking.

### Database design

Choose relational database:
- Works well with frequent-reads and infruequent-writes
- Provides `ACID`, which is important for a reservation system. Otherwise things like negative balance, double charge, double resertvations can occur.
- Makes app logic easier

Design tables for the following entity:
1. **hotel**: hotel_id (PK), name, address, location
2. **room**: room_id (PK), room_type_id, floor, number, hotel_id, name, is_available
3. **room_type_rate**: hotel_id (PK), date (PK), rate
4. **guest**: guest_id (PK), first_name, last_name, email
5. **reservation**: reservation_id (PK), hotel_id, room_type_id, start_date, end_date, status, guest_id
6. **room_type_inventory**: hotel_id (PK), room_type_id (PK), date (PK), total_inventory, total_reserved

- 1 & 2 are part of "Hotel Service"
- 3 & 4 are part of Rate and Guest services, respectively.
- 5 & 6 are part of "Reservation Service"

For 2 years, room_type_inventory will be 5K hotels x 20 types of room types x 2 x 365 days = 73 million rows. Enough for a single DB, but to avoid single point-of-failure, add DB replications in multiple regions or availability zones.

**SQL statements:**
```sql
SELECT date, total_inventory, total_reserved
FROM room_type_inventory
WHERE room_type_id = ${roomTypeId} AND hotel_id = ${hotelId}
AND date between ${startDate} and ${endDate}
```

Check conditions by taking into consideration to overbooking factor (i.e. multiply total inventory by 110%).

**Scalability**
- Store only current and future reservation data, move past data to archive
- Sharding on hotel ID

**Concurrency Issues**
1. UI deterrent: Disable submit once clicked
2. Use idempotency key to avoid double creation by the same user (DB constraint)
3. `Pessimistic Locking`: Lock selected rows by using `SELECT ... FOR UPDATE`
   - Pros: Easy to implement, useful when data connection is heavy (high concurrency)
   - Cons: Deadlocks may occur, not very scalable (--> not recommended here)
4. `Optimistic Locking`: Add a "version" column, which is incemented by the app by 1 when writing to the row, and checked by the DB via validation check (or transaction will be aborted)
   - Pros: More performant than pessimistic locking .
   - Cons: Performance drops drammatically when concurrency is high.
5. `Database constraints`: Similar to optimistic locking. Add a constraint using `CONSTRAINT ... CHECK` to ensure total_inventory - total_reserved >= 0. 
   - Cons: Cannot be version-controlled easily in app code, not all DBs support it

**Caching**
- Use cache for DBs , eg. Redis
- Use TTL to expire old data automatically 
- Use LRU cache-eviction policy
- Pros: Performance
- Cons: Data consistency (an available room may already be reserved)