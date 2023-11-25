// App.js

import React, { useState } from 'react';
import BookingForm from './BookingForm';

function App() {
  const [bookings, setBookings] = useState([]);

  const handleBookingSubmit = (newBooking) => {
    setBookings([...bookings, newBooking]);
  };

  return (
    <div className="app">
      <h1>Little Lemon Restaurant</h1>
      <BookingForm onSubmit={handleBookingSubmit} />
      <h2>Bookings</h2>
      <ul>
        {bookings.map((booking, index) => (
          <li key={index}>{`Table for ${booking.numPeople} on ${booking.date} at ${booking.time}`}</li>
        ))}
      </ul>
    </div>
  );
}

export default App;


// BookingForm.js

import React, { useState } from 'react';

function BookingForm({ onSubmit }) {
  const [numPeople, setNumPeople] = useState('');
  const [date, setDate] = useState('');
  const [time, setTime] = useState('');

  const handleSubmit = (e) => {
    e.preventDefault();
    if (numPeople && date && time) {
      const newBooking = { numPeople, date, time };
      onSubmit(newBooking);
      setNumPeople('');
      setDate('');
      setTime('');
    } else {
      alert('Please fill in all fields');
    }
  };

  return (
    <form onSubmit={handleSubmit}>
      <label>
        Number of People:
        <input type="number" value={numPeople} onChange={(e) => setNumPeople(e.target.value)} />
      </label>
      <label>
        Date:
        <input type="date" value={date} onChange={(e) => setDate(e.target.value)} />
      </label>
      <label>
        Time:
        <input type="time" value={time} onChange={(e) => setTime(e.target.value)} />
      </label>
      <button type="submit">Book Table</button>
    </form>
  );
}

export default BookingForm;
