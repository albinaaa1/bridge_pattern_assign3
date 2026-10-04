# Assignment 3: Bridge Pattern Implementation

* **Student Name:** Onlasyn Albina Adiletqyzy
* **Group:** SE-2527
* **Topic:** Option B — Notifications
* **Repository URL:** https://github.com/albinaaa1/bridge_pattern_ass3](https://github.com/albinaaa1/bridge_pattern_assign3)

---

## Role Map

| Pattern Role | Entity Name | Source Path | Key Methods / Locations |
| :--- | :--- | :--- | :--- |
| **Abstraction** | `Notification` | `src/Notification.java` | Base class storing `Channel` field, `execute()`, `setImplementation()` |
| **Refined Abstraction A1** | `Reminder` | `src/Reminder.java` | Extends `Notification`, formats reminder message |
| **Refined Abstraction A2** | `UrgentAlert` | `src/UrgentAlert.java` | Extends `Notification`, formats urgent message |
| **Implementor** | `Channel` | `src/Channel.java` | Interface defining `send(String content)` |
| **Concrete Implementor I1**| `EmailChannel` | `src/EmailChannel.java` | Implements `send()` with email envelope |
| **Concrete Implementor I2**| `SmsChannel` | `src/SmsChannel.java` | Implements `send()` with SMS prefix |
| **Concrete Implementor I3**| `PushChannel` | `src/PushChannel.java` | Extension class implementing `send()` with push envelope |
| **Client** | `Main` | `src/Main.java` | Standard entry point executing T1–T7 checks |

---

## Key Method Locations

* **Bridge Field:** `protected Channel channel;` in `src/Notification.java`
* **Execute Method:** `execute()` in `src/Notification.java` (implemented in `Reminder.java` and `UrgentAlert.java`)
* **Set Implementation:** `setImplementation(Channel channel)` in `src/Notification.java`
* **Runtime Switch Check:** Demonstrated in test `T5` within `src/Main.java`

---

## Build & Run Commands

From the project root folder:
## Expected Demonstration Outcomes (T1–T7)

```text
T1 PASS | Reminder + EmailChannel | result=[Email Envelope] Reminder: Meeting at 3 PM
T2 PASS | Reminder + SmsChannel | result=SMS: Reminder: Meeting at 3 PM
T3 PASS | UrgentAlert + EmailChannel | result=[Email Envelope] URGENT: Server down!
T4 PASS | UrgentAlert + SmsChannel | result=SMS: URGENT: Server down!
T5 PASS sameObject=true | stateUnchanged=true
  before=[Email Envelope] Reminder: Pay electricity bill
  after=SMS: Reminder: Pay electricity bill
T6 PASS | Reminder + PushChannel | result=[Push Envelope] Reminder: Doctor appointment
T7 PASS | UrgentAlert + PushChannel | result=[Push Envelope] URGENT: Security breach!
SUMMARY: 7/7 PASS


```bash
javac -release 17 -encoding UTF-8 -d out "@sources.txt"
java -cp out Main
