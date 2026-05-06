## Hotfix Lifecycle & Consolidated Hotfix Git Flow

In real-world scenarios, different customers may use different versions of the product, so multiple release branches are maintained, such as release/1.2.2. Each customer is mapped to a specific release branch rather than the main development branch.

A hotfix is a quick fix applied to resolve critical issues in a specific production version. When an issue is identified in version 1.2.2 (for example, a customer facing a bug in release/1.2.2), a hotfix branch is created from the corresponding release branch, not from the main branch. The fix is implemented, tested by QA, and deployed to the affected customer.

After deployment, the fix is cherry-picked into the main branch to ensure future releases include the change.

A consolidated hotfix (CHF) refers to grouping multiple fixes together and deploying them in a single release to reduce deployment effort and improve efficiency.

Customers currently face challenges such as managing multiple branches, identifying the correct version for fixes, ensuring proper testing, and maintaining coordination between QA, frontend, and backend teams.

The application solves this by providing a structured workflow to select the correct issue, map it to the appropriate branch, manage fixes, and track deployment with full traceability.

It also ensures that all teams are aligned on the same workflow, reducing miscommunication and improving reliability of hotfix delivery.

Overall, this approach simplifies hotfix management and ensures faster, controlled, and error-free production fixes.

---

## Hotfix vs Consolidated Hotfix Flow

```mermaid id="vertical_flow_fix"
flowchart TD

%% -------- HOTFIX FLOW --------
subgraph HOTFIX
    A1["Customer Issue in Production Version 1.2.2"]
    A2["Bugs Tab Select BUG-101"]
    A3["Build and Wrap Select Repo and release 1.2.2"]
    A4["Generate Branch"]
    A5["hotfix 1.2.2 BUG-101"]
    A6["Developer Fixes Code in GitHub"]
    A7["QA Validation"]
    A8["Build and Deploy via Workbench"]
    A9["Merge to release 1.2.2"]
    A10["Cherry pick to main"]

    A1 --> A2 --> A3 --> A4 --> A5 --> A6 --> A7 --> A8 --> A9 --> A10
end

%% spacer connection to force vertical layout
A10 --> B1

%% -------- CHF FLOW --------
subgraph CHF
    B1["Multiple Customer Issues Version 1.2.2"]
    B2["Bugs Tab Select Multiple Bugs"]
    B3["Build and Wrap Select Repo and release 1.2.2"]
    B4["Generate CHF Branch"]
    B5["chf 1.2.2 batch1"]
    B6["Developers Fix All Issues in GitHub"]
    B7["QA Tests All Fixes Together"]
    B8["Single Build and Deploy"]
    B9["Merge to release 1.2.2"]
    B10["Cherry pick all fixes to main"]

    B1 --> B2 --> B3 --> B4 --> B5 --> B6 --> B7 --> B8 --> B9 --> B10
end
```

---

## Consolidated Hotfix Git Flow

```mermaid id="gitgraph_chf_flow"
gitGraph
   commit id:"main init"

   branch release-1.2.2
   checkout release-1.2.2
   commit id:"release 1.2.2"

   branch wb-chf-1.2.2-batch1
   checkout wb-chf-1.2.2-batch1
   commit id:"CHF branch created via Workbench"

   commit id:"fix BUG-101 UI"
   commit id:"fix BUG-102 API"
   commit id:"fix BUG-103 validation"

   commit id:"QA validated all fixes"

   checkout release-1.2.2
   merge wb-chf-1.2.2-batch1 tag:"CHF deployed"

   checkout main
   merge wb-chf-1.2.2-batch1 tag:"all fixes synced"
```
