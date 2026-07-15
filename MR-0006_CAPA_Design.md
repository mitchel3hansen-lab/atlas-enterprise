# MR-0006 --- CAPA Management

## Objective

Implement a complete Corrective and Preventive Action (CAPA) module that
extends the Investigation workflow into verification, effectiveness
review, and final closure.

## Database

### capa_actions

-   id (UUID)
-   tenant_id
-   incident_id
-   investigation_id
-   capa_number
-   action_type (Corrective \| Preventive)
-   title
-   description
-   owner_id
-   department
-   priority
-   target_date
-   completed_date
-   status
-   verification_status
-   effectiveness_status
-   estimated_cost
-   actual_cost
-   created_at
-   updated_at

### capa_evidence

-   id
-   capa_id
-   evidence_type
-   title
-   reference_uri
-   uploaded_by
-   uploaded_at

### capa_verifications

-   verifier_id
-   verified_at
-   result
-   notes

### capa_effectiveness_reviews

-   reviewer_id
-   review_date
-   result
-   recurrence_found
-   comments

## API Endpoints

POST /api/capas GET /api/capas GET /api/capas/{id} PUT /api/capas/{id}
POST /api/capas/{id}/complete POST /api/capas/{id}/verify POST
/api/capas/{id}/effectiveness POST /api/capas/{id}/reopen

## Workflow

Incident → Investigation → CAPA → Verification → Effectiveness Review →
Closure

## Completion Gates

A CAPA cannot close until:

-   Owner completes action
-   Evidence uploaded
-   Safety verification passes
-   Effectiveness review completed
-   Executive approval (configurable)

## Dashboard KPIs

-   Open CAPAs
-   Overdue CAPAs
-   Average completion days
-   Verification pass rate
-   Effectiveness rate
-   CAPAs by department
-   CAPAs by severity
-   Estimated cost avoided

## Notifications

-   30-day reminder
-   14-day reminder
-   7-day reminder
-   Due today
-   Overdue escalation

## Acceptance Criteria

-   Multiple CAPAs may be linked to one investigation.
-   Every CAPA has an owner and due date.
-   Verification and effectiveness are stored separately.
-   Failed verification returns the CAPA to In Progress.
-   Every state transition creates a timeline event.
