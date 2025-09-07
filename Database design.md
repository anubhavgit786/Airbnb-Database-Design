### 2. **Hotel**

* Fields: `id`, `name`, `city`, `active`, `photos[]`, `amenities[]`
* Embedded: `contactInfo` (address, phone, email, location)
* Relationships:

  * 1 Hotel → *many* Rooms
  * 1 Hotel → *many* Inventories
  * 1 Hotel → *many* Bookings

---

### 3. **Room**

* Fields: `id`, `type` (single, double, deluxe), `basePrice`, `totalCount`, `capacity`, `photos[]`, `amenities[]`
* Relationships:

  * Belongs to **1 Hotel**
  * 1 Room → *many* Inventories
  * 1 Room → *many* Bookings

---

### 4. **Inventory**

* Fields: `id`, `hotel_id`, `room_id`, `date`, `bookedCount`, `totalCount`, `surgeFactor`, `price`, `city`, `closed`
* Unique constraint: (`hotel_id`, `room_id`, `date`) ✅ ensures ek din ke liye ek hi record
* Yeh table **availability aur pricing** handle karta hai.

---

### 5. **Booking**

* Fields: `id`, `bookingStatus`, `roomsCount`, `checkInDate`, `checkOutDate`
* Relationships:

  * Belongs to **1 Hotel**
  * Belongs to **1 Room**
  * Belongs to **1 User**
  * May have **1 Payment**
  * Many-to-Many with Guests (ek booking me multiple guests ho sakte hain)

---

### 6. **Guest**

* Fields: `id`, `age`, `gender`
* Belongs to **1 User** (means guest ka master user hota hai)
* Used in **Booking** as `booking_guest` join table

---

### 7. **Payment**

* Fields: `id`, `transactionId`, `status`, `amount`
* 1 Payment → *1 Booking*

---