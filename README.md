# Experiment-8
# study the system specifications of an ATM system and report any identified bugs.
# Purpose

To analyse the system specifications of an ATM (Automated Teller Machine) system and produce a clear record of identified/likely bugs, their impact, severity, reproduction hints, and suggested fixes — formatted so it can be attached to project records or handed to developers/testers.

# Scope

This report covers the typical software, hardware and integration behaviours of an ATM system as derived from standard ATM functional requirements — including account access, cash withdrawal, deposits (if supported), balance inquiry, PIN management, transaction logging, network communications with the bank host, UI flows, and peripheral control (card reader, cash dispenser, printer, keypad, touch screen).

# Intended Audience

* QA/Test engineers
* ATM software developers
* System architects / integrators
* Bank operations and security teams
* Project managers and product owners

# Product Perspective

The ATM is an embedded/edge device that interfaces with:

* Bank host/switch over a secure network (ISO 8583 or similar)
* Card/payment network (EMV, chip, magstripe)
* Peripherals: card reader, PIN pad, cash dispenser, deposit unit, printer, touchscreen/display, receipt printer, sensors (door/tilt)
* Local OS (RTOS / Windows Embedded / Linux) and middleware for transaction processing
  It must meet regulatory and security requirements (PCI, EMV, local banking laws).

# Product Functions (high-level)

1. Card insertion/verification (EMV/magstripe)
2. PIN entry & verification (offline/online)
3. Account selection and transaction types (withdrawal, deposit, transfer, balance inquiry)
4. Cash dispensing with counting/validation and cash-out confirmation
5. Receipt printing / digital receipt option
6. Transaction logging/audit and host messaging (request/response/settlement)
7. Error handling and safe-fail modes (jackpot prevention, out-of-service)
8. Session timeout/idle management and card retention on errors
9. Software updates and configuration management (remote)
10. Accessibility features (audio, large text)

# Operating Environments

* Physically: indoor/outdoor kiosks with variable temperatures and humidity
* Network: WAN/LAN with intermittent connectivity; requires retries and offline-safe behaviours
* Power: mains with battery/UPS for safe shutdown
* Security: physically adversarial environment — tamper, skimming, fraud attempts

# Design / Implementation Constraints

* Real-time responses for user interactions and host timeouts
* Strong cryptographic requirements (PIN encryption, EMV keys) and secure key management
* Memory/storage constraints in embedded hardware
* Regulatory compliance: PCI-DSS, EMV, anti-money-laundering logging
* Deterministic handling of cash and dispenser state to prevent loss (double dispense, jam)
* Firmware signing and update safety to prevent rogue updates

# Assumptions and Dependencies

* Bank host adheres to expected message formats and responses (e.g., ISO 8583).
* Peripherals provide correct status codes and can be polled.
* Clock/time is synchronized (for logs, non-repudiation).
* Physical hardware previously validated (cash cassette, sensors).
* Network latency and failure scenarios are handled by retry/backoff policies.

# Possible Bugs on an ATM Machine

Double Cash Dispense – ATM dispenses money twice due to retry or network delay.

Incorrect PIN Validation – PIN retry counter not updating or PIN accepted incorrectly.

Card Reader Malfunction – Card not read properly or card ejected unexpectedly.

Cash Cassette Empty Error – ATM shows enough cash but dispenser is empty.

Receipt Printer Issues – Out-of-paper errors not detected or blank receipts printed.

UI Freezing – Screen hangs during transaction or buttons unresponsive.

Network Timeout Errors – Transaction stuck due to poor host communication.

Incorrect Balance Display – Balance shown on ATM not matching bank server.

EMV Chip Error Handling – ATM falls back to magstripe insecurely.

Cash Jam in Dispenser – ATM counts cash but fails to deliver notes.

Session Timeout Too Fast – ATM cancels transaction even when user is active.

Wrong Language/Display Issues – Text not fully visible or wrong language shown.

Failed Reversal – Amount debited even though cash not dispensed.

Incorrect Logging – Transaction logs missing or not saved properly.

Security Bugs – PIN displayed/viewable, weak encryption, or log leaks.

# Result 

The analysis of the ATM system specifications identified several critical, medium, and minor bugs related to security, transaction handling, hardware sensors, and user interface behaviour. These findings highlight the need for improvements in reliability, accuracy, and overall system robustness.

