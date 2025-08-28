# Analysis of Architectural Approaches for Right to Work (RTW) Verification

## Overview

As we prepare to implement VEVO verification and anticipate future requirements like the US E-Verify system, it is crucial to adopt a robust and maintainable architecture for our Right to Work (RTW) functionality.

This document evaluates two primary approaches to determine the most effective long-term solution:

- Leveraging our existing YAML-based framework.
- Developing a dedicated, separate logic module for RTW.


## 📄 System Design Principles Analysis

| Design Principle              | Option 1 (YAML Framework)                         | Option 2 (Dedicated Module)                        |
| :---------------------------- | :------------------------------------------------ | :------------------------------------------------- |
| **Separation of Concerns** | ❌ Tightly coupled, high risk of regressions.     | ✅ Decoupled and isolated, minimal risk.           |
| **Maintainability** | ⚠️ High complexity, difficult to modify.          | ✅ Simple, focused, and easy to maintain.          |
| **Flexibility & Extensibility** | ⚠️ Constrained by existing framework.             | ✅ Unrestricted, designed for future growth.       |
| **Reusability** | ✅ High reuse of existing components.             | ⚠️ New components built from scratch.              |


## 📄 Business & Development Impact

| Perspective | Option 1: Use YAML for RTW | Option 2: Separate Logic for RTW |
|-------------|----------------------------|----------------------------------|
| **Initial Investment & Delivery Speed** | `Lower initial cost.` This approach leverages existing components for faster delivery with less immediate development effort. | `Higher initial investment.` Requires new module development from the ground up, resulting in a slower initial delivery. |
| **Scalability & Cost of Changes/Modifications** | `Constrained by the existing framework.` Future modifications are more complex and costly, as checked with the existing architecture (currently `1,500+` lines of yaml configurations). | `High flexibility for future features.` Full control over the logic makes implementing new requirements (like E-Verify later on) or customisations cheaper, faster. |
| **Dependencies** | `Cross-System Impact`: Relies on the ESS module, meaning extra testing efforts requireed. | `Isolated Scope`: The logic is fully self-contained, easier for testing independently. |

## 📄 Detailed Technical Implementation

A detailed breakdown of the technical implementation for both options is available on the following Confluence page [link](https://deputy.atlassian.net/wiki/spaces/hr/pages/4801757473/RAPID+-+Usage+of+YAML+for+RTW+Employee+Manager+Experience)

## 🎤 Conclusion & Strategic Choice

The choice between these options represents a classic trade-off between short-term velocity and long-term architectural health.

- Option 1 (YAML Framework) prioritises speed and a lower initial cost. It is the faster path to market but introduces significant long-term risk and technical debt due to its tight coupling with the existing framework.

- Option 2 (Dedicated Module) requires a greater upfront investment but delivers a clean, decoupled architecture. This approach significantly reduces long-term maintenance costs and provides the flexibility to adapt to future requirements efficiently and safely.

In a word, our decision depends on whether we are optimising for a quick delivery or for the future scalability and customisable of our RTW system.
