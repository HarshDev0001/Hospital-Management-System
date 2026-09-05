Software Requirements Specification

Hospital Management System

Project: Hospital Management System

Version: 1.1

Authors:HARSH RAJ ( PES2UG24CS184), DASARI VINAY (PES2UG24CS145) , DIYA
J MARAR (PES2UG24CS162), CHRIS KHUSHNAM (PES2UG24CS139)

Date: 03-09-2026

Status: Draft For Review

### Revision history

### Approvals

## Table of Contents

1.  Introduction

2.  Overall description

3.  External interfaces

4.  System features (detailed)

5.  Non-functional requirements (detailed)

6.  Quality attributes & Acceptance tests

## 7. System models and diagrams

### 7.1 UML Use-Case Diagrams

Two use-case diagrams are provided for the Hospital Management System.

**Figure 1 --- Patient workflow handled through Reception**

![Figure 1 -- Patient workflow handled through
Reception](images/use-case-diagram-patient-reception.png)

**Figure 2 --- Receptionist, Doctor, Admin, and Lab/Pharmacy Staff
interactions**

![Figure 2 -- Staff use cases](images/use-case-diagram-staff.png)

8.  Requirements Traceability Matrix (RTM)

## 1. Introduction

### 1.1 Purpose

This document is a Software Requirements Specification (SRS) for a
Hospital Management System (HMS). It defines the functional and
non-functional requirements, interfaces, and verification criteria for a
patient record and appointment management system for hospitals, intended
for instructors and students to use as a reference and for the
development team to implement against.

### 1.2 Scope

Covers patient registration, medical record maintenance, appointment
scheduling for doctors/departments, doctor and staff consultation
workflows, billing and payments, basic pharmacy/laboratory
record-keeping, and administrative reporting for a single hospital or
clinic. The system is implemented in C/C++ as a single-user,
single-machine application (see Section 2.5). Excludes integration with
external insurance-provider systems, national health-record registries,
in-patient admission/discharge, and full hospital ERP functions
(HR/payroll, procurement) beyond what is listed above.

### 1.3 Audience

Developers, QA Engineers, Hospital Administrators, Reception Staff,
Doctors, Lab/Pharmacy Staff, and Assessment Evaluators.

### 1.4 Definitions

List of acronyms: HMS (Hospital Management System), UHID (Unique
Health/Hospital ID), EMR (Electronic Medical Record), OPD (Out-Patient
Department), UI (User Interface), API (Application Programming
Interface), RBAC (Role-Based Access Control), DB (Database), PII
(Personally Identifiable Information).

## 2. Overall description

### 2.1 Product perspective

The HMS is a standalone desktop/console-based application (C/C++) backed
by a local, file-based or lightweight relational database. It is a new,
self-contained product; it is not a modification of an existing legacy
system for the scope of this mini project.

### 2.2 Major product functions

Patient registration and medical record management

Appointment scheduling, rescheduling, and cancellation

Doctor/staff profile management and OPD queue view

Consultation recording (diagnosis, prescriptions, recommended tests)

Billing, payment recording, and receipt generation

Basic laboratory result entry and pharmacy dispensing

Administrative master-data management, system configuration, and summary
reporting

### 2.3 User roles and characteristics

Patient: provides demographic information and appointment requests
through reception; does not directly access the system or use a login of
their own.

Receptionist: frequent daily use, needs fast registration and booking
screens.

Doctor: needs a clear daily queue and quick access to patient history
during consultation.

Lab / Pharmacy Staff: needs to update results/stock against specific
orders/prescriptions.

Hospital Admin: manages master data, staff accounts, system
configuration, and views reports; needs oversight rather than
transactional speed.

### 2.4 Operating environment

Desktop/console environment running on a standard PC (Windows/Linux),
developed in C/C++ with a local file-based or lightweight relational
database for persistence. Single-hospital / single-site deployment for
the scope of this mini project. Only one user session is active on the
system at a time; the application does not provide concurrent multi-user
or networked access (see Section 2.5 and Section 3.4). No dedicated
hardware beyond a standard workstation and printer for receipts is
assumed.

### 2.5 Constraints

Single-user, single-machine operation: only one active session runs on
one workstation at a time. Multi-user concurrent access and network /
client-server deployment are explicitly out of scope for this mini
project (see Section 3.4); requirements and diagrams elsewhere in this
document are written to be consistent with this decision.

Implementation language restricted to C / C++ as per the project brief.

Data-privacy handling for patient medical information (see Section 5.1
Security).

Limited team size and academic-semester timeline restrict scope to the
modules listed in Section 2.2.

No dependency on paid third-party services; any external interface is
optional/stubbed for demonstration purposes.

## 3. External interface requirements

### 3.1 User interfaces

Primary UI: a menu-driven console interface (or a simple desktop GUI if
implemented) with clear, numbered options for each role (Reception,
Doctor, Lab/Pharmacy, Admin). Every staff role reaches its menu only
after Secure Login (HMS-F-024). Input validation messages and
confirmation prompts are shown before any data-changing action.

### 3.2 Hardware interfaces

Standard PC keyboard and display for data entry and viewing

Optional receipt/bill printer

Optional barcode/ID scanner for Patient ID lookup (future enhancement,
not mandatory for this mini project)

### 3.3 Software interfaces

Local database engine (e.g., file-based storage or a lightweight
relational database accessed via C/C++ file I/O or a DB library) for
persisting patients, appointments, staff, billing, and records.

Optional export interface to generate reports/receipts as text or CSV
files for printing.

### 3.4 Communications

The system is a single-machine, single-user application for the scope of
this mini project: all data entry, processing, and storage occur on one
workstation.

No network communication or client-server protocol is required or
implemented. This is a firm scope decision (see Section 2.5); it
supersedes any wording elsewhere that could be read as implying
concurrent multi-user or online/networked access.

\<\< This SRS defines 21 functional requirements (Section 4), 5
non-functional requirements (Section 5), 3 security objectives, and 5
security requirements (Section 5.1), meeting the minimum of 15 FRs / 5
NFRs / 2 security objectives / 5 security requirements. \>\>

## 4. System features (detailed)

Each requirement below includes acceptance criteria and a reference test
case. IDs follow HMS-F-###.

### 4.1 Patient Registration & Records Management

Description: Capture patient demographic and medical data, assign a
unique identifier, and maintain a searchable, updatable medical record.
IDs follow HMS-F-001..HMS-F-004.

### 4.2 Appointment Scheduling

Description: Allow reception staff to book, reschedule, and cancel
appointments against a doctor's available slots without conflicts. IDs
follow HMS-F-010..HMS-F-013.

### 4.3 Doctor / Staff Management & Consultation

Description: Authenticate staff, maintain doctor and staff profiles,
present each doctor's daily queue, and record consultation outcomes. IDs
follow HMS-F-020..HMS-F-024.

### 4.4 Billing & Payments

Description: Generate itemized bills for a patient visit, record
payments, and issue receipts. IDs follow HMS-F-030..HMS-F-032.

### 4.5 Pharmacy & Laboratory

Description: Support diagnostic result entry and pharmacy dispensing
linked to a patient visit and prescription. IDs follow
HMS-F-040..HMS-F-041.

### 4.6 Administration & Reporting

Description: Maintain hospital master data, system configuration, and
provide management-level summary reports. IDs follow
HMS-F-050..HMS-F-052.

## 5. Non-functional requirements (detailed)

NFRs below are measurable and tied to test plans. IDs follow HMS-NF-###.

### 5.1 Security

#### 5.1.1 Security Objectives

Confidentiality: protect patient medical records and PII from
unauthorized access, both at rest and in use.

Integrity: ensure medical records, prescriptions, and billing data can
only be modified by authorized users, with all changes auditable.

Availability: keep critical patient-care functions (registration,
appointment booking, record retrieval) accessible during hospital
operating hours despite common failure or misuse scenarios.

#### 5.1.2 Security Requirements

## 6. Quality attributes & Acceptance tests

Exit criteria for acceptance: all high-priority functional requirements
implemented and verified, no critical NFR failures, and the RTM (Section
8) shows all listed test cases passed.

Acceptance test suites: Patient Registration, Appointment Scheduling,
Authentication & Access Control, Consultation & Records, Billing,
Pharmacy/Lab, Performance, and Security.

## 7. System models and diagrams

### 7.1 UML Use-Case diagrams

Two use-case diagrams are provided: one showing the patient workflow
handled indirectly through Reception, and one covering the internal
hospital-staff use cases (Receptionist, Doctor, Admin, Lab/Pharmacy
Staff). Both diagrams have been revised to match the requirements in
Section 4 and the single-user, single-machine scope in Section 2.5. The
staff diagram includes Secure Login (HMS-F-024) and Configure System
Parameters (HMS-F-052), with representative \<`<include>`{=html}\>
relationships shown.

## 8. Requirements Traceability Matrix (RTM)

Every requirement in Sections 4 and 5 is traced below to its defining
section, implementing module, and reference test case(s). Status: N =
Not implemented, P = In progress, A = Accepted.
