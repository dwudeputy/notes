# Proposed solution for YAML for RTW vs Separate Logic for RTW

Hi team, after read few confluence pages + codebases general checking, also later on, we might need to do E-Verify (US RTW). 

Acorrding to the initial analysis, we might need to come up with a robust and extendable/maintainable solution for handling this VEVO + E-Verify RTW part of functionality development.



## ✅ Comparison Table (with 4 angles)

| Perspective | Option 1: Use YAML for RTW | Option 2: Separate Logic for RTW |
|-------------|----------------------------|----------------------------------|
| **Development Cost (Business)** | Lower upfront cost – reuses existing components and YAML rules. `Faster delivery`, less effort needed now. | Higher upfront cost – `building from scratch`, more development + testing needed. Slower delivery. |
| **Code Maintenance (Development)** | Lower ongoing effort as long as ESS/YAML stays stable. But`tightly coupled` → changes in ESS logic may force retesting RTW (Extra testing efforts required). | Slightly higher maintenance overhead (new codebase to maintain), but isolated from ESS changes → `less risk of unexpected breakages`. |
| **Ease of Modification / Cost of Future Changes (Business + Development)** | Harder to modify – changes must fit into existing YAML/json-rules-engine complexity. Current line of yaml configurations is `1500`. | Easier to modify – full control of RTW logic. `Future changes/customizations are cheaper and less risky`. |
| **CUE Debug (Development)** | multiple resources to start – debug requires to start `multiple resources` eg: svc-hr + fe-nomono codebases for reproduce bug locally (slower)  | Easier to reproduce bug – in local, just reproduce the bug from Frontend codebase (fe-nomono) in local environment (`faster`). |

## 📄 Compare with technical implmentations

The details could be found via confluence page [link](https://deputy.atlassian.net/wiki/spaces/hr/pages/4801757473/RAPID+-+Usage+of+YAML+for+RTW+Employee+Manager+Experience)

## 🎤 Quick Summary

Option 1 (YAML) = cheaper & faster now, but changes later are harder and risky due to dependency on ESS/YAML.

Option 2 (Separate logic) = more expensive now, but much easier and cheaper to evolve later, with cleaner separation of concerns.
