# Error Reconciliation Module

## Overview
The **Error Reconciliation Module** is a critical component in the **Quantum Key Distribution (QKD)** system, designed to ensure consistency between Alice and Bob's keys while detecting potential security breaches. Errors may arise due to measurement discrepancies, environmental interference, or eavesdropping. The module includes two key components:
- **Error Correction (EC):** Uses the Cascade protocol for reconciling discrepancies.
- **Error Verification (EV):** Employs Toeplitz hashing to verify key integrity.

Key features:
- Operates on frames of **8192 bits** each, processing up to **128 frames** (1048576 bits) in total.
- Monitors information leakage and the number of error bits corrected to maintain system security.

---

## Error Correction (EC)

### Process Overview
The error correction process reconciles differences between Alice and Bob's sifted keys without revealing the full key content. It uses the **Cascade Protocol** for parity-based correction.

- **Alice's Role:** Responds to parity requests from Bob, reshuffles the key to its original form, and ensures security by recording information leakage and error bits.  
- **Bob's Role:** Iteratively adjusts row indices to identify and correct errors. Utilizes the error bit count from the previous frame to set initial conditions for the next frame.

### Implementation
Key modules in the Cascade Protocol architecture:
- **Shuffle**: Randomizes key order to prevent pattern recognition.
- **Parity Tree**: Computes and compares parities.
- **Control Module**: Manages state transitions.
- **TXRX I/O**: Facilitates data exchange between Alice and Bob.

#### Reconciliation Efficiency (RE)
The efficiency of error correction is measured by the reconciliation efficiency ($RE$), which evaluates the amount of leaked information relative to the QBER. Smaller initial row indices improve latency and maintain acceptable $RE$ levels.

| **Initial Row Index** | **Error Bits Count** |
|------------------------|----------------------|
| 7                      | 0–98                |
| 6                      | 99–204              |
| 5                      | 205–520             |
| 4                      | 521–8192            |

---

## Error Verification (EV)

### Process Overview
After error correction, the EV module reduces the likelihood of mismatches by comparing hash tags generated via **Toeplitz hashing**. If hash tags match, the frame is written to the reconciled key; otherwise, it is discarded.

- **Alice's Role:** Prepares and transmits hash tags and error bit counts to Bob.
- **Bob's Role:** Compares received hash tags with locally generated ones and confirms consistency.

### Specifications
| **Parameter**               | **Value**             |
|-----------------------------|-----------------------|
| Input Frame Size ($n$)      | 8192 bits            |
| Output Hash Tag Size ($m$)  | 32 bits              |
| Toeplitz Hashing            | Matrix Multiplication |
| MAC Units                   | 32                   |
| Word Width                  | 32 bits              |

---

## Key Features
- **Error Correction:** High-performance reconciliation using the Cascade protocol with efficient information leakage monitoring.
- **Error Verification:** Robust integrity checks via Toeplitz hashing and random bits.
- **Latency Optimization:** Dynamic row index adjustments based on QBER to enhance reconciliation speed.

---

## Figures and Block Diagrams

### Error Reconciliation Workflow
![圖片](https://github.com/user-attachments/assets/1001ea91-3d32-4064-9385-48a521151c9f)

### Cascade Protocol Architecture
![圖片](https://github.com/user-attachments/assets/27c36cc3-1f96-4793-9d69-5fd8c6537589)

### Alice's EC Module
- **Flow Chart**:  
![圖片](https://github.com/user-attachments/assets/3966ab3f-ea9e-4763-9770-1fc1cf3c40d3)
- **Block Diagram**:  
![圖片](https://github.com/user-attachments/assets/11b457f0-787e-4efb-bd61-78c7f96bf7bf)
- **Detailed I/O**:  
![圖片](https://github.com/user-attachments/assets/50c1c8b6-2670-4ff6-9ded-11cf105ed54e)

### Bob's EC Module
- **Flow Chart**:  
![圖片](https://github.com/user-attachments/assets/feed8a9f-a688-4afc-989b-237efd10e7ff)
- **Block Diagram**:  
![圖片](https://github.com/user-attachments/assets/d65c98a3-7b1e-4cc2-a405-6514d88b2276)
- **Detailed I/O**:  
![圖片](https://github.com/user-attachments/assets/02130058-3912-49b9-9b1b-8391c6be7c39)

### Error Verification Workflow
![圖片](https://github.com/user-attachments/assets/e021b17c-e6b8-4b33-9319-826a5f5ef086)

### Alice's EV Module
- **Block Diagram**:  
![圖片](https://github.com/user-attachments/assets/11f94155-fe81-44ee-a20a-178cadc1fd4d)
- **Detailed I/O**:  
![圖片](https://github.com/user-attachments/assets/a0dde5e4-1ebc-4562-97b9-d36c5ba8e9b5)

### Bob's EV Module
- **Block Diagram**:  
![圖片](https://github.com/user-attachments/assets/ade4fd5e-4422-4551-bc06-008b88de601f)
- **Detailed I/O**:  
![圖片](https://github.com/user-attachments/assets/a8b478ea-f238-4b7d-a6d2-17a52f52b6c5)
