CareIT

Project Overview

AI-Powered Triage
- Patients input symptoms in free-form text
- NLP-based triage recommends the most relevant medical specialty
- Provides transparent rationale and allows user override for safety and control

Doctor Discovery System
- Maps patient needs to available practitioners using geospatial search
- Integrates OpenStreetMap (Overpass API + Nominatim) for real-world provider data
- Graceful fallback to seeded database ensures system reliability

Appointment Booking
- Lightweight scheduling system with real-time availability
- Secure storage of bookings with patient/doctor associations
- Enforced data integrity through backend constraints

AI SOAP Note Generation
- Converts clinical conversation transcripts into structured SOAP notes:
- Subjective
- Objective
- Assessment
- Plan
- Ensures clinician oversight with mandatory review step before approval

Human-in-the-Loop Validation
- Doctors can edit and approve AI-generated clinical documentation
- System enforces approval gating at the API level (not just UI)
- Prevents unverified clinical data from being exported

FHIR-Compatible Export Pipeline
- Generates deterministic FHIR R4 JSON bundles from approved encounters:
- Consent resources
- Composition (SOAP note)
- MedicationRequest (when applicable)
- Ensures interoperability with modern EMR systems
- Controlled-substance logic enforced at serialization layer

Core Flow:
- Patient submits symptom description
- AI triage recommends specialty
- System retrieves nearby doctors (or fallback dataset)
- Patient books appointment
- Doctor conducts encounter and generates SOAP note
- Doctor reviews and approves documentation
- System exports FHIR-compliant medical record bundle

Why it matters:

Healthcare systems in clinical settings are often fragmented, manual, and difficult to scale for small providers. This project demonstrates how AI can responsibly:
- Reduce administrative workload for clinicians
- Improve patient routing efficiency
- Standardize messy clinical documentation
- Enable interoperability with modern healthcare systems

Features:
- Voice → text intake
- AI structuring into medical format
- FHIR-compatible output

My Role:

Database Engineer (Eric Cariaga)
- Designed and implemented Supabase database schema for patient, doctor, and appointment workflows
- Built Python-based backend integration layer to interface with Supabase
- Enforced booking integrity with DB-level uniqueness constraints to prevent double-bookings
- Implemented validation logic and lightweight API wrappers for safe read/write operations
- Supported reliable local development setup and database reset/migration workflows for the team

Tech Stack:
- Frontend: Next.js 14, React 18, TypeScript, Tailwind CSS
- API: FastAPI, Pydantic
- Core Logic: Python 3.12+ (`dataclasses`, deterministic processing)
- Database: Supabase (PostgreSQL)
- Interoperability: FHIR R4 JSON Bundle

Hackathon Context:
- Built during CareDevi AI Hackathon with a team.
- Original prompt in HACKATHON.md

Demo Walkthrough (Screenshots)

1. Front page
![Front page](Demo/01-frontPage.png)

2. Login page
![Login page](Demo/02-loginPage.png)

3. Patient searches for a doctor
![Patient searches doctor](Demo/03-patientSearchDoctor.png)

4. AI symptom intake
![AI symptom intake](Demo/04-AI.symptomIntake.png)

5. Patient chooses a doctor
![Choose doctor](Demo/05-chooseDoctor.png)

6. Patient books a time slot
![Book time slot](Demo/06-bookTimeSlot.png)

7. Booking success confirmation
![Booking success](Demo/07-successBook.png)

8. Patient joins consultation
![Patient joins consultation](Demo/07.1-patientJoinConsultation.png)

9. Doctor dashboard
![Doctor dashboard](Demo/08-doctorDashboard.png)

10. Doctor pastes consultation history
![Doctor pastes consultation history](Demo/09-doctorPastesConsultationHistory.png)

11. SOAP guided notes
![SOAP guided notes](Demo/010-soapGuidedNotes.png)

12. Verification and FHIR export
![Verification and FHIR export](Demo/011-verificationAndFHIRexport.png)