# Test Plan – Workbench Application (API + UI End-to-End)



## 1. Overview

This test plan covers end-to-end validation of the Workbench application across API and UI layers. The goal is to ensure core workflows function correctly, API responses are accurate, and the UI reflects expected behavior consistently.

---

## 2. Scope

### In Scope

- API validation (status codes, response structure, data correctness)
- UI validation (user flows, data display, form behavior)
- End-to-end testing (UI action → API call → UI result)
- Functional testing of all core workflows

### Out of Scope

- Performance / load testing
- Advanced security testing
- Authentication testing (not part of current system)

---

## 3. Features to be Tested

### 3.1 Application Access

| # | Test Scenario | Type |
|---|---|---|
| 1 | Open Workbench URL and verify page loads | UI |
| 2 | Verify all main sections are visible on load | UI |
| 3 | Verify no console errors on load | UI |

---

### 3.2 Project Creation

| # | Test Scenario | Type |
|---|---|---|
| 1 | Create a new project via UI with valid data | UI + API |
| 2 | Validate `POST /workbench/insert-project-details` request and response | API |
| 3 | Verify newly created project appears in the project list | UI |
| 4 | Attempt to create a project with missing required fields | UI |
| 5 | Verify API returns correct error for invalid input | API |

---

### 3.3 Bug Linking

| # | Test Scenario | Type |
|---|---|---|
| 1 | Link one or more bugs/issues to an existing project | UI + API |
| 2 | Validate `POST /workbench/insert-project-jira-bugs` request and response | API |
| 3 | Verify linked bugs are displayed correctly in the project view | UI |
| 4 | Validate `GET /workbench/get-project-jira-bugs` returns correct data | API |
| 5 | Attempt to link a bug to a non-existent project | API |

---

### 3.4 Branch & Commit Suggestions

| # | Test Scenario | Type |
|---|---|---|
| 1 | Select an issue and generate a branch name | UI + API |
| 2 | Validate `GET /llm/generate_gh_branch_name` response | API |
| 3 | Verify generated branch name is displayed in UI | UI |
| 4 | Trigger commit suggestions for selected issues | UI + API |
| 5 | Validate `POST /llm/jira-cherry-pick-commits` response | API |
| 6 | Verify commit suggestions appear correctly in UI | UI |

---

### 3.5 GitHub Operations

| # | Test Scenario | Type |
|---|---|---|
| 1 | Fetch and display list of branches | UI + API |
| 2 | Validate `GET /github/branches` response | API |
| 3 | Compare two branches and verify diff is displayed | UI + API |
| 4 | Validate `GET /github/compare` response | API |
| 5 | Fetch commits and verify display in UI | UI + API |
| 6 | Validate `GET /github/commits` response | API |

---

### 3.6 Performance Assessment

| # | Test Scenario | Type |
|---|---|---|
| 1 | Navigate to performance tab | UI |
| 2 | Apply filter by Developer role | UI + API |
| 3 | Apply filter by QA role | UI + API |
| 4 | Validate API response for filtered data | API |
| 5 | Verify correct data is displayed after filtering | UI |
| 6 | Verify spider/radar chart renders correctly | UI |

---

### 3.7 Self Review & Manager Review

| # | Test Scenario | Type |
|---|---|---|
| 1 | Fill and submit self-review form with valid data | UI + API |
| 2 | Validate API submission request and response | API |
| 3 | Verify submitted data is saved and displayed correctly | UI |
| 4 | Fill and submit manager review form | UI + API |
| 5 | Verify manager review data is reflected in UI | UI |
| 6 | Attempt to submit review form with missing required fields | UI |

---

### 3.8 Settings & Configuration

| # | Test Scenario | Type |
|---|---|---|
| 1 | Open settings and verify all config sections load | UI |
| 2 | Update GitHub configuration and save | UI + API |
| 3 | Validate `POST /workbench/config/github/set` | API |
| 4 | Update Jira configuration and save | UI + API |
| 5 | Validate `POST /workbench/config/jira/set` | API |
| 6 | Update LLM configuration and save | UI + API |
| 7 | Validate `POST /workbench/config/llm/set` | API |

---

### 3.9 License

| # | Test Scenario | Type |
|---|---|---|
| 1 | Verify license status is displayed correctly | UI |
| 2 | Verify license expiry notification appears when appropriate | UI |

---

## 4. Test Approach

### API Testing

- Validate HTTP status codes (`200`, `201`, `400`, `404`, `500`)
- Validate response body structure and field values
- Validate error responses for invalid/missing inputs

**Tools:**
- Robot Framework API Tests

---

### UI Testing

- Validate user flows match expected behavior
- Validate form inputs, validations, and error messages
- Validate data displayed matches API responses

**Tools:**
- Robot Framework
- Selenium

---

### Example Flows

| Flow | Validation |
|---|---|
| Create project | `POST /workbench/insert-project-details` → project visible in list |
| Link bug | `POST /workbench/insert-project-jira-bugs` → bug shown in project view |
| Submit review | API call → data saved and visible in UI |

---

## 5. Test Data

| Data Type | Description |
|---|---|
| Project data | Sample project name, product, version, dates |
| Bug/issue data | Valid Jira issue keys for linking |
| GitHub data | Branch names, commit hashes for comparison |
| Performance data | Developer/QA entries for filtering |
| Review form data | Valid inputs for self and manager review |
| Config data | GitHub token, Jira credentials, LLM settings |

---

## 6. API Endpoints Reference

| Endpoint | Method | Feature |
|---|---|---|
| `/workbench/insert-project-details` | POST | Create project |
| `/workbench/get-all-project-details` | GET | Get all projects |
| `/workbench/insert-project-jira-bugs` | POST | Link bugs |
| `/workbench/get-project-jira-bugs` | GET | Get linked bugs |
| `/workbench/update-project-status` | GET | Update status |
| `/workbench/config/github/set` | POST | Set GitHub config |
| `/workbench/config/jira/set` | POST | Set Jira config |
| `/workbench/config/llm/set` | POST | Set LLM config |
| `/github/branches` | GET | List branches |
| `/github/commits` | GET | List commits |
| `/github/compare` | GET | Compare branches |
| `/jira/issues` | GET | Fetch Jira issues |
| `/llm/generate_gh_branch_name` | GET | Generate branch name |
| `/llm/jira-cherry-pick-commits` | POST | Cherry-pick suggestions |

---

## 7. Challenges / Considerations

- Mapping UI actions to exact backend API calls
- Managing consistent and reusable test data
- Validating dynamic data (LLM suggestions, performance metrics)
- Some API responses depend on external services (GitHub, Jira, LLM)

---

## 8. Notes

- This plan is aligned with actual application features and API endpoints
- Authentication is not included as it is not part of the current system
- Test scenarios will be refined further as specifications are finalized
- Detailed test cases will be derived from this plan in the next phase
- Existing Robot Framework tests in `robot-tests/` can be used as a base reference

---

## 9. Reporting and Logging

### Reports Generated

- Test execution reports
- Automation logs
- Failure screenshots
- API execution logs

### Failure Handling

- Screenshot capture on failure
- Detailed error logging
- Stack trace logging

---

## 10. Framework Design Principles

The automation framework follows the below principles:

- Modularity
- Reusability
- Scalability
- Maintainability
- Separation of concerns

---

## 11. CI/CD Integration

### Objective

To support automated execution in CI/CD pipelines.

### Supported Platforms

- Jenkins
- GitHub Actions
- GitLab CI

### CI/CD Validations

- Automated test execution
- Scheduled execution
- Report generation
- Failure notifications

---
