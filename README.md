    ""# Automated Doctor Scheduling Smart Contract

This is a Move smart contract for an **Automated Doctor Scheduling dApp** built on the Aptos blockchain. The contract allows doctors to create schedules with available appointment slots and lets patients book those slots securely.

## Functionalities

1. **create\_schedule**

   * Allows a doctor to create an appointment schedule with a specified number of available slots.
   * Stores the schedule on the blockchain under the doctor's address.

   **Parameters:**

   * `doctor`: The signer's address representing the doctor.
   * `slots`: The number of available appointment slots.

   **Usage Example:**

   ```move
   AutomatedScheduling::DoctorScheduler::create_schedule(&signer, 10);
   ```

2. **book\_appointment**

   * Allows a patient to book an available slot from a doctor's schedule.
   * Reduces the available slots count and emits an event.

   **Parameters:**

   * `patient`: The signer's address representing the patient.
   * `doctor`: The address of the doctor whose schedule is being booked.

   **Usage Example:**

   ```move
   AutomatedScheduling::DoctorScheduler::book_appointment(&signer, 0xDoctorAddress);
   ```

## Events

* **AppointmentBookedEvent**:

  * Emitted when a patient successfully books an appointment.
  * Contains:

    * `patient`: The address of the patient who booked.
    * `slots_remaining`: The remaining available slots after booking.

## Deployment

To deploy this contract:

1. Compile the module.
2. Deploy it to the Aptos blockchain with the appropriate signer.
3. Interact using the Move CLI or Aptos Explorer.

## Testing

You can use Move Prover and Aptos CLI to test interactions:

```bash
move test
```

## License

MIT License
""
