    ""module AutomatedScheduling::DoctorScheduler {

    use aptos_framework::signer;
    use aptos_framework::event;

    /// Struct representing a doctor's schedule.
    struct Schedule has store, key {
        slots_available: u64,
    }   

    /// Event for booking confirmation.
    struct AppointmentBookedEvent has drop, store {
        patient: address,
        slots_remaining: u64,
    }

    /// Event handle for appointment booking.
    struct AppointmentEvents has store {
        event_handle: event::EventHandle<AppointmentBookedEvent>,
    }

    /// Function for doctors to create their available schedule.
    public fun create_schedule(doctor: &signer, slots: u64) {
        let schedule = Schedule {
            slots_available: slots,
        };
        move_to(doctor, schedule);

        let event_handle = AppointmentEvents {
            event_handle: event::new_event_handle<AppointmentBookedEvent>(doctor),
        };
        move_to(doctor, event_handle);
    }

    /// Function for patients to book an available slot.
    public fun book_appointment(patient: &signer, doctor: address) acquires Schedule, AppointmentEvents {
        let schedule = borrow_global_mut<Schedule>(doctor);
        let events = borrow_global_mut<AppointmentEvents>(doctor);

        assert!(schedule.slots_available > 0, 0x1); // Ensure slots are available
        schedule.slots_available = schedule.slots_available - 1;

        event::emit_event(
            &mut events.event_handle,
            AppointmentBookedEvent {
                patient: signer::address_of(patient),
                slots_remaining: schedule.slots_available,
            }
        );
    }
}""
