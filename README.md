# 🛡️ API Security Mastery: Week 1 Research
**Project Goal:** Mapping Hidden Attack Surfaces & Tech Fingerprinting

## 📊 Executive Summary (Management Brief)
In my research this week, I focused on **Information Leakage** and **Parameter Inconsistency**. 
* **The Risk:** Many APIs have "invisible" logic that differs from what the security layer (WAF) sees.
* **Business Impact:** If our WAF and Backend interpret data differently, attackers can bypass security filters.
* **Strategic Value:** Identifying these "Logic Fingerprints" allows us to build more resilient, context-aware defenses.

---

## 🔬 Technical Research: The "Logic Fingerprint" Guide
I documented how different backend architectures react when receiving duplicate parameters (e.g., `?id=123&id=456`).

| Backend Tech | Observation | Security Risk |
| :--- | :--- | :--- |
| **Node.js (Express)** | Returns an **Array** | Can cause logic crashes or "Type Confusion." |
| **Python (Flask)** | Takes the **First** value | Bypasses filters checking the second value. |
| **PHP / Apache** | Takes the **Last** value | Bypasses filters checking the first value. |
| **Java (Spring)** | **Joins** them (`1,456`) | Bypasses "Exact Match" security rules. |

## 🕵️‍♂️ Proof of Concept: Hidden Parameter Discovery
**Discovery Method:** HTTP Parameter Pollution (HPP)
**Finding:** By injecting `?admin=true` into a standard user profile request, we test if the backend "auto-maps" unauthorized administrative fields to our session.
