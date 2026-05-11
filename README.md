# Serial Communication Standards: RS-232 vs. RS-422 vs. RS-485

This repository provides a technical overview and comparison of the three most common asynchronous serial communication standards used in computing and industrial automation.

---

## 1. Quick Comparison Table

| Feature | RS-232 | RS-422 | RS-485 |
| :--- | :--- | :--- | :--- |
| **Mode of Operation** | Single-Ended | Differential | Differential |
| **Network Topology** | Point-to-Point | Multi-drop | Multi-point |
| **Max. Drivers** | 1 | 1 | 32 (Standard) / up to 256 |
| **Max. Receivers** | 1 | 10 | 32 (Standard) / up to 256 |
| **Max. Cable Length** | $15\text{ m}$ ($50\text{ ft}$) | $1,200\text{ m}$ ($4,000\text{ ft}$) | $1,200\text{ m}$ ($4,000\text{ ft}$) |
| **Max. Data Rate** | $20\text{ kbps}$ (Standard) | $10\text{ Mbps}$ | $10\text{ Mbps}$ |
| **Standard Voltage** | $\pm 5\text{V}$ to $\pm 15\text{V}$ | $\pm 2\text{V}$ to $\pm 6\text{V}$ | $\pm 1.5\text{V}$ to $\pm 6\text{V}$ |
| **Duplex** | Full Duplex | Full Duplex | Half or Full Duplex |

---

## 2. RS-232: The Legacy Desktop Standard
Introduced in 1960, RS-232 was designed to connect a **DTE** (Data Terminal Equipment, e.g., a PC) to a **DCE** (Data Circuit-terminating Equipment, e.g., a modem).

*   **How it works:** It uses **single-ended signaling**, where the signal voltage is measured relative to a common ground (GND).
*   **Strengths:** Universal compatibility with older hardware, simple 3-wire setup (TX, RX, GND) for basic communication.
*   **Weaknesses:** 
    *   **Noise Sensitivity:** Ground loops and electrical noise easily corrupt data since the reference is a single ground wire.
    *   **Distance:** Signal degradation limits it to short cable runs.

---

## 3. RS-422: High-Speed Multi-Drop
RS-422 improved upon RS-232 by introducing **differential signaling** (balanced signaling) to achieve higher speeds and longer distances.

*   **How it works:** It transmits signals over a pair of wires ($A$ and $B$). The receiver calculates the difference: $V_{diff} = V_A - V_B$.
*   **Noise Immunity:** Because noise usually affects both wires equally (Common Mode Noise), the differential calculation cancels it out.
*   **Network:** Supports a "Master-Slave" configuration. One driver can talk to up to 10 receivers, but the receivers cannot talk back to the master on the same line.

---

## 4. RS-485: The Industrial Workhorse
RS-485 is the industry standard for robust, multi-device networking, commonly used with protocols like **Modbus**.

*   **Multi-point Capability:** Unlike RS-422, RS-485 drivers can be placed in a high-impedance state (tri-state), allowing multiple transmitters to share the same wire pair.
*   **2-Wire vs. 4-Wire:**
    *   **2-Wire (Half-Duplex):** Reduced wiring costs; devices must "take turns" talking.
    *   **4-Wire (Full-Duplex):** Simultaneous transmit and receive, similar to RS-422 but with multiple masters possible.
*   **Termination:** To prevent signal reflection on long cables, a $120\,\Omega$ resistor is typically placed at the two extreme ends of the bus.

---

## 5. Technical Deep Dive

### Differential Signaling Logic
In RS-422 and RS-485, the binary state is determined by:
*   **Logic 0 (Space):** $V_A < V_B$ (Differential voltage is negative).
*   **Logic 1 (Mark):** $V_A > V_B$ (Differential voltage is positive).

### The Unit Load (UL) Concept
In RS-485, the "32 device limit" is based on **Unit Loads**. Standard transceivers represent $1$ UL. Modern high-impedance transceivers represent $1/4$ or $1/8$ UL, allowing up to **256 devices** on a single bus segment.

### Speed vs. Distance Relationship
There is always a trade-off. While these standards can reach $1,200\text{ m}$, they cannot do so at $10\text{ Mbps}$. 
*   At $1,200\text{ m}$, the max rate is typically $\approx 100\text{ kbps}$.
*   To achieve $10\text{ Mbps}$, the cable length usually must be under $10\text{ m}$.

---

## Summary: Which to Choose?

1.  **RS-232:** Best for simple, short-range PC-to-device connections (Console ports, Lab equipment).
2.  **RS-422:** Best for long-distance point-to-point or one-way broadcast to multiple displays/receivers.
3.  **RS-485:** Best for industrial environments, complex sensor networks, and scenarios where wiring cost/complexity must be minimized.
