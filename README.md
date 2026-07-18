# relay-logic_2026-07-18
System overview
An external trigger source (sensor, switch, or PLC signal) feeds into an existing control PCB that drives two relay outputs. Relay 1 is designed to follow the trigger live — energizing while the trigger is active and de-energizing when it releases. Relay 2 is intended to be a one-shot timer: it should energize on trigger, run for a fixed preset duration, then de-energize automatically — regardless of whether the trigger is still held or has already released.

Current fault
The board has a logic bug causing Relay 2 to ignore its own timer and instead track the trigger signal exactly like Relay 1. If the trigger is held longer than the preset time, Relay 2 stays energized the entire time. If the trigger is released early, Relay 2 drops immediately. This breaks the intended timed-latch behavior.

Proposed scope
Diagnose and repair the existing PCB — not a ground-up redesign. The fix involves isolating Relay 2's drive logic from the raw trigger line and restoring its independent timing path (whether that is a discrete 555 monostable stage, a microcontroller timer routine, or dedicated timer IC logic). After repair, the board will be bench-tested to verify:
Relay 1 still follows the trigger faithfully.
Relay 2 fires once per trigger edge and self-terminates after the preset interval.

Proof of understanding
To demonstrate clarity on the exact fault before touching hardware, an interactive browser-based simulation was built. It lets you hold the trigger, switch between the current broken behavior and the corrected fixed behavior, and watch the relays and their loads respond in real time — including a live countdown timer for Relay 2's one-shot duration.

Deliverable
A repaired, tested control board where Relay 2 operates as a true independent one-shot timer, ready to drop back into your system.
