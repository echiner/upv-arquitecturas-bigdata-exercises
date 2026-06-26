# Exercise 1: Enterprise Architectural Design Case Studies

## Objective
In this exercise, you will design high-level architectures for three diverse enterprise use cases. Your designs must leverage modern architectural paradigms (e.g., real-time streaming, modern cloud data platforms, and AI-centric workflows) and address core requirements such as scalability, responsiveness, governance, and compliance.

## Instructions
1.  **Select a Tool**: Choose any diagramming tool to create your architectures (e.g., [Draw.io](https://draw.io), [Excalidraw](https://excalidraw.com), PowerPoint, or Mermaid.js).
2.  **Design the Architectures**: For each of the three cases below, create a high-level architectural diagram.
3.  **Document Your Decisions**: Write a brief justification for your design choices. Explain:
    *   The flow of data from source to destination.
    *   The selected technologies (e.g., message brokers, databases, orchestration, AI services).
    *   How your design satisfies the business and technical constraints of the case study.
4.  **Submission**: Submit your diagrams along with your documentation (in Markdown or PDF format).

---

## Case Studies

### Case 1: The Intelligent Fleet (Real-Time / Streaming)

#### Business Context
**"FlashMove"** is a rapidly growing micro-mobility company operating a fleet of 50,000 connected electric scooters and e-bikes across 15 major European cities. To stay competitive, optimize operations, and ensure user safety, the company needs to transition from daily batch processing to an architecture driven by real-time events.

#### Core Requirements
*   **High-Velocity Data Ingestion**: Each vehicle transmits telemetry data (GPS coordinates, battery level, speed, braking intensity, and component temperature) every 5 seconds when in use.
*   **Immediate Operational Actions**:
    *   The system must detect geofencing violations (e.g., a user entering a pedestrian-only zone) within less than 2 seconds to automatically trigger a speed reduction command back to the vehicle.
    *   It must trigger instant alerts for maintenance crews if a vehicle reports a sudden battery drop or a critical hardware failure code.
*   **Dynamic Pricing & Demand Forecasting**: The business wants to implement a dynamic pricing engine that changes rental rates minute-by-minute based on current vehicle availability and historical demand in specific city quadrants.
*   **Long-Term Analytics**: Data must be retained for long-term historical analysis (to detect city-wide usage patterns and predict component degradation over months).

---

### Case 2: The Omni-Channel Retailer (Data-Centric & Modern Cloud)

#### Business Context
**"Veloce Style"** is a traditional fashion retailer that has expanded into e-commerce, resulting in massive data silos. Their inventory systems, physical Point-of-Sale (PoS) terminals, e-commerce platform, and customer loyalty mobile app all live in disconnected environments. They want a modern, unified, cloud-based data architecture to treat data as a core product.

#### Core Requirements
*   **The "Single Source of Truth"**: The business needs a unified view of customer behavior across both digital and physical touchpoints. A purchase in a physical store should immediately reflect in the customer's online profile.
*   **Analytical Profiles**: Business analysts and data scientists need to run complex, ad-hoc queries combining years of historical sales transactions with unstructured web traffic logs (clickstream data) to build personalized recommendation engines.
*   **Data Democratic Access**: Different departments (Marketing, Finance, Supply Chain) require autonomous access to specific datasets. However, the data must remain centralized conceptually to avoid duplicating storage costs and creating conflicting metrics.
*   **Scalability & Cost Optimization**: Sales exhibit massive seasonal spikes (e.g., Black Friday). The architecture must scale up effortlessly to handle a 20x increase in transactional volume and scale down automatically to minimize costs during quiet periods.

---

### Case 3: Next-Gen Digital Healthcare (AI & Governance Heavy)

#### Business Context
**"SanoCare"** is a digital health provider offering remote patient monitoring and virtual consultations. They are designing a new platform that utilizes artificial intelligence to assist doctors with early diagnoses and patient care. Because they handle highly sensitive medical records, strict regulatory compliance and robust governance are non-negotiable.

#### Core Requirements
*   **AI-Assisted Diagnostics**: The platform needs to ingest multi-modal data—structured patient electronic health records (EHR), unstructured doctor notes, and high-resolution medical imaging (DICOM files). An AI model will analyze this data to flag potential cardiovascular anomalies for the doctor's review.
*   **AI Guardrails & Explainability**: Doctors must be able to see why the AI flagged a specific patient (lineage of the decision). The system must guarantee that the AI models do not suffer from hallucinations or bias against specific demographic groups.
*   **Strict Data Privacy (GDPR/HIPAA Compliance)**: Personally Identifiable Information (PII) and medical history must be strictly segregated, heavily encrypted, and masked. Access must be granted based on rigid, role-based permissions (e.g., a researcher can see anonymized trends, but only the primary doctor can see patient names).
*   **Data Auditability**: The organization requires an automated way to track the complete lifecycle of a data point—from the moment a medical image is uploaded, through how it was used to train or evaluate an AI model, down to who accessed it.

---
[⬅ Back to Module 1 README](./README.md)
