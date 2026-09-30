# Implement Client Script & UI Policy – Incident Management

## Project Overview

This project demonstrates the implementation of ServiceNow UI Policies, UI Policy Actions, and Client Scripts to control and validate Incident records.

The main purpose is to improve Incident data quality and consistency by making fields mandatory based on conditions, automatically setting field values, controlling field behavior, validating information before submission, and preventing unwanted list-based updates.

## Objectives

- Improve Incident data accuracy and consistency.
- Make fields mandatory based on specific conditions.
- Automatically populate field values.
- Control field behavior dynamically.
- Validate Incident information before submission.
- Prevent restricted list-based updates.
- Provide appropriate messages to users.

## Technologies Used

- ServiceNow
- Incident Management
- UI Policy
- UI Policy Actions
- Client Scripts
- JavaScript
- Form Validation
- Data Validation

## Project Phases

### Phase 1 – Requirement Analysis

The project focuses on controlling Incident form behavior and maintaining accurate Incident information using UI Policies, UI Policy Actions, Client Scripts, JavaScript, and form validation.

Major requirements include:
- Conditional mandatory fields
- Automatic field value setting
- Dynamic field behavior
- Form validation
- Prevention of unauthorized list updates

### Phase 2 – UI Policy Configuration

#### High Impact Control

A UI Policy named **High Impact Control** is configured on the Incident table.

**Condition:** Impact = 1 – High

**Action:** Assignment group = Mandatory

When an Incident has High Impact, the Assignment group field becomes mandatory. When the condition becomes false, the mandatory behavior is reversed.

### Phase 3 – UI Policy Action for Urgency

A UI Policy Action is configured for the **Urgency** field.

**Condition:** Impact = 1 – High

**Action:** Urgency = Read-only

When an Incident is classified as High Impact, users can view the Urgency value but cannot modify it.

### Phase 4 – onChange Client Script

#### Auto Set Urgency for High Impact

This Client Script automatically sets the Urgency field to High when the Impact field is changed to High.

**Configuration:**
- Table: Incident
- Type: onChange
- Field: Impact
- Active: True

When Impact = 1 – High, the script sets Urgency to 1 – High and displays an information message.

### Phase 5 – onSubmit Client Script

#### Prevent Save if Assigned To Missing

This Client Script validates the **Assigned To** field before an Incident is submitted.

**Condition:**
- Impact = High
- Assigned To = Empty

If both conditions are true:
- An error message is displayed.
- The Incident record is not saved.
- The user must provide an Assigned To value.

**Validation Message:**

> Assigned To is mandatory for High impact incidents.

### Phase 6 – onCellEdit Client Script

#### Prevent State Change via List Edit

This Client Script prevents users from changing the **State** field directly through Incident list editing.

**Configuration:**
- Table: Incident
- Type: onCellEdit
- Field: State
- Active: True

When a user attempts to edit State from the list, an alert is displayed and the update is blocked. The user must open the Incident form to change the State.

**Alert Message:**

> State cannot be updated using list editing. Please open the Incident.

## Testing & Validation

The implemented configurations were tested using multiple scenarios.

| Test Case | Scenario | Expected Result | Status |
|---|---|---|---|
| TC01 | High Impact + Assigned To empty | Record should not save | Pass |
| TC02 | High Impact + Assigned To populated | Record should save | Pass |
| TC03 | Change Impact from High to Medium | UI Policy behavior should reverse | Pass |
| TC04 | Change State using list edit | Update should be blocked | Pass |
| TC05 | Change State from Incident form | State change should save | Pass |

## Final Outcome

The project demonstrates:
- Conditional mandatory fields
- Automatic urgency assignment
- Read-only field control
- Save-time validation
- List-edit restrictions
- Dynamic reversal of UI behavior
- Improved Incident data consistency
- Better control over Incident form interactions

## Conclusion

The **Implement Client Script & UI Policy – Incident Management** project demonstrates how ServiceNow UI Policies and Client Scripts can be used to improve data quality, consistency, and user interaction.

UI Policies dynamically control field behavior based on defined conditions, while `onChange`, `onSubmit`, and `onCellEdit` Client Scripts provide automation, validation, and control over user actions.

The completed solution helps ensure that Incident records contain the required information before submission and reduces inappropriate or unintended list-based modifications.

## Project Skills

- ServiceNow Incident Management
- UI Policy Configuration
- UI Policy Actions
- Client Scripts
- JavaScript
- Form Validation
- Incident Form Configuration
- Data Validation

## Project Structure

```text
ServiceNow-Incident-UI-Policy-Client-Script/
│
├── README.md
│
├── Phase-1/
│   └── Requirement Analysis
│
├── Phase-2/
│   └── High Impact UI Policy
│
├── Phase-3/
│   └── Urgency UI Policy Action
│
├── Phase-4/
│   └── Auto Set Urgency onChange Client Script
│
├── Phase-5/
│   └── Prevent Save onSubmit Client Script
│
├── Phase-6/
│   └── Prevent State Change onCellEdit Client Script
│
└── Phase-7/
    └── Testing, Validation & Conclusion
```
