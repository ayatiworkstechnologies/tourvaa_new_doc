# Chapter 28: Frontend Architecture & User Experience Quality Audit

## Executive Summary

This Frontend & UX Quality Audit evaluates the component architecture, state management patterns, routing mechanisms, mobile responsiveness, accessibility standards, and interface performance across [`tourvaa-admin-frontend`](../tourvaa-admin-frontend). The frontend comprises **163 App Router pages** spanning the Public Storefront and five authenticated portals (Admin, Supplier, Customer, Agent, Affiliate).

```mermaid
flowchart TD
    subgraph Root["Next.js App Router (src/app/)"]
        LAYOUT["Root Layout (layout.tsx)"]
        AUTH_PROV["AuthProvider (User, Tokens, Role)"]
        CURR_PROV["CurrencyProvider (USD, EUR, GBP, AUD)"]
        QUERY_CLIENT["TanStack Query Client Provider"]
    end

    subgraph Portals["Multi-Portal Layout Trees"]
        PUB_TREE["(public) Layout -> Header, Footer, ChatWidget"]
        ADMIN_TREE["admin Layout -> AdminSidebar, AdminRouteGuard"]
        SUP_TREE["supplier Layout -> SupplierHeader, ProtectedRoute"]
        AGT_TREE["agent Layout -> AgentHeader, ProtectedRoute"]
        CUST_TREE["customer Layout -> CustomerHeader, ProtectedRoute"]
        AFF_TREE["affiliate Layout -> AffiliateHeader, ProtectedRoute"]
    end

    subgraph UX_Audit_Nodes["Audit Focus Areas"]
        G1["Hydration Timing: SSR Dropdown Click Race Condition"]
        G2["Form Usability: Raw useState vs React Hook Form"]
        G3["Image Optimization: HTML img vs Next Image"]
        G4["Accessibility: Custom Selects Missing ARIA Attributes"]
    end

    LAYOUT --> AUTH_PROV
    AUTH_PROV --> CURR_PROV
    CURR_PROV --> QUERY_CLIENT
    QUERY_CLIENT --> PUB_TREE
    QUERY_CLIENT --> ADMIN_TREE
    QUERY_CLIENT --> SUP_TREE
    QUERY_CLIENT --> AGT_TREE
    QUERY_CLIENT --> CUST_TREE
    QUERY_CLIENT --> AFF_TREE

    PUB_TREE -.-> G1
    ADMIN_TREE -.-> G2
    PUB_TREE -.-> G3
    ADMIN_TREE -.-> G4
```

---

## 1. Architectural & UX Findings

### 1.1 SSR Hydration Timing on Interactive Dropdowns
- **Severity**: **Medium**
- **Location**: [`src/components/public/PublicHeader.tsx`](../tourvaa-admin-frontend/src/components/public/PublicHeader.tsx) and [`e2e/homepage-ui-ux.spec.ts:43-49`](../tourvaa-admin-frontend/e2e/homepage-ui-ux.spec.ts#L43-L49)
- **Evidence**: The Playwright test suite documents a known timing issue:
  ```typescript
  // Hydration-safe: on a dev server the SSR button can be clicked before
  // React attaches onClick, so retry until the dropdown actually opens.
  const dropdown = page.locator(".profile-dropdown-panel");
  await expect(async () => {
    if (!(await dropdown.isVisible())) await profileBtn.click();
    await expect(dropdown).toBeVisible();
  }).toPass({ timeout: 15000 });
  ```
- **Finding**: During the initial page load on low-bandwidth mobile connections, the server-side rendered profile dropdown button displays immediately, but clicking it before JavaScript finishes hydration results in dropped click events.
- **Remediation**: Render interactive buttons in disabled or skeleton state until client-side hydration completes, or implement progressive enhancement using native HTML `<details>` and `<summary>` elements that toggle without JavaScript.

### 1.2 Form Validation Strategy Inconsistency
- **Severity**: **Medium**
- **Location**: [`src/components/settings/ApiSettingsSection.tsx`](../tourvaa-admin-frontend/src/components/settings/ApiSettingsSection.tsx) vs [`src/components/tours/TourPricingTab.tsx`](../tourvaa-admin-frontend/src/components/tours/TourPricingTab.tsx)
- **Finding**: While complex modules (such as Tour Management) use React Hook Form with Zod schemas ([`lib/utils/validators.ts`](../tourvaa-admin-frontend/src/lib/utils/validators.ts)), several administrative settings tabs (API Settings, Email Templates, Currency Rules) manage form state via fragmented individual `useState` hooks.
- **Impact**: Form validation errors are reported post-submission via server API error toasts rather than providing immediate inline field validation during input typing.
- **Remediation**: Standardize all forms on React Hook Form and Zod schemas to ensure unified inline error messaging and touched/dirty state tracking.

### 1.3 Image Optimization Across Storefront
- **Severity**: **Medium**
- **Location**: [`src/components/public/LegalPageLayout.tsx`](../tourvaa-admin-frontend/src/components/public/LegalPageLayout.tsx), [`src/components/public/home/`](../tourvaa-admin-frontend/src/components/public/home)
- **Finding**: Certain banner hero sections and CMS blog article cards render standard HTML `<img src="..." />` tags rather than Next.js `<Image />` components.
- **Impact**: Misses automatic WebP/AVIF format conversion, viewport-responsive `srcset` generation, and layout-shift prevention (`width`/`height` aspect ratio placeholders). This reduces Lighthouse performance scores and increases mobile data transfer.
- **Remediation**: Replace raw `<img>` tags with `next/image` with configured `sizes` attributes and remote image domains in `next.config.js`.

### 1.4 Accessibility (a11y) & Keyboard Navigation
- **Severity**: **Low**
- **Location**: [`src/components/ui/SearchableSelect.tsx`](../tourvaa-admin-frontend/src/components/ui/SearchableSelect.tsx)
- **Finding**: Custom dropdown menus and autocomplete widgets lack complete WAI-ARIA combobox attributes:
  - Missing `aria-expanded` toggling on open/close
  - Missing `aria-activedescendant` during arrow-key navigation
  - Dropdown options lack `role="option"` with `aria-selected`
- **Impact**: Screen readers cannot announce current dropdown state or highlighted options to visually impaired users.
- **Remediation**: Implement Headless UI or Radix UI primitives for all dropdown, dialog, and combobox interactions.

---

## 2. Interface State Handling Audit

| State Type | Current Implementation | Evaluation & Coverage |
|---|---|---|
| **Loading States** | Reusable [`Loader.tsx`](../tourvaa-admin-frontend/src/components/common) component and skeleton placeholders used across tables and dashboard metrics. | **Good (85% Coverage)**: Most data tables show a clear loading indicator during TanStack Query fetching. |
| **Empty States** | Empty state illustrations and informative messages ("No bookings found", "No active payouts") present in major views. | **Good (90% Coverage)**: Actionable "Create Tour" or "Invite Agent" buttons are provided on empty list views. |
| **Error States** | Global Axios response interceptor displays floating alert toasts; layout error boundaries (`error.tsx`) catch rendering panics. | **Acceptable (75% Coverage)**: Some settings tabs fail silently or only log to console when secondary lookup calls fail. |

---

## 3. State Management Architecture

The frontend correctly avoids monolithic global stores (e.g. Redux) in favor of a clean, decoupled state architecture:
1. **Server State**: Managed via TanStack Query with automatic cache invalidation (`queryClient.invalidateQueries({ queryKey: [...] })`) upon mutations.
2. **Authentication & Session**: Centralized in [`AuthProvider.tsx`](../tourvaa-admin-frontend/src/providers/AuthProvider.tsx) with dual-cookie sync.
3. **Currency & Localization**: Managed via `CurrencyProvider.tsx` with dynamic price calculation helpers.
4. **Local UI State**: Kept local to individual components via React `useState` and `useReducer`.
