# Problem Bank: React & Browser Fundamentals

This problem bank supports the React & Browser Fundamentals interviewer. Use the walkthroughs to guide discussion without revealing the solution before the requested hint level.

## Problem 1: Predict the Event Loop

### Problem Statement

Given synchronous logging, a zero-delay timer, and a resolved promise, ask the candidate to predict output order and explain the call stack, task queue, and microtask queue.

### Solution Walkthrough

The synchronous statements run first. Once the current stack is empty, the browser drains microtasks, so the promise callback runs before the timer task. The expected order is `A`, `D`, `C`, `B`.

### Follow-up Questions

- What happens if a microtask continuously queues another microtask?
- Why can a long synchronous task make a page feel frozen even when the network is fast?
- When would `requestAnimationFrame` be preferable to a timer?

## Problem 2: Build a Race-Free Autocomplete

### Problem Statement

Design a React autocomplete that debounces input, handles loading/error/empty states, supports keyboard navigation, and never displays a response for an older query after a newer query has completed.

### Solution Walkthrough

Keep the input value, request status, options, and active option separate or model them as a clear state machine. Debounce the request, create an `AbortController` for each request, abort it in effect cleanup, and ignore an `AbortError`. A request ID or query comparison can provide an additional stale-response guard.

The input should use a native label and combobox semantics. When suggestions are visible, expose `aria-expanded`, `aria-controls`, and `aria-activedescendant`; render options in a listbox; support ArrowUp, ArrowDown, Enter, and Escape; and announce status changes when needed.

### Follow-up Questions

- How would you test out-of-order responses deterministically?
- How would virtualization affect active-option IDs and scrolling?
- Would you put server results in context, local state, or a query cache? Why?

## Problem 3: Design an Accessible Modal

### Problem Statement

Design a modal that can be opened with a button, has an accessible name, traps focus while open, closes with Escape, and restores focus when closed.

### Solution Walkthrough

Prefer the native `<dialog>` element when its behavior and browser support meet the requirements; otherwise implement the dialog contract carefully. Use a portal if necessary to avoid stacking-context problems, but preserve the relationship to the opener in application state.

On open, save `document.activeElement`, move focus to a meaningful control, and prevent Tab from leaving the dialog. Close on Escape and restore focus if the opener still exists. Add `aria-labelledby` and `aria-modal="true"` for a custom dialog, label the close button, and ensure the background cannot be accidentally operated by keyboard or pointer. Manage scroll locking without a visible layout shift.

### Follow-up Questions

- How should nested dialogs be represented?
- What should happen if the opener is removed while the dialog is open?
- Which tests verify keyboard behavior and screen-reader semantics?

## Problem 4: Diagnose a Slow Product List

### Problem Statement

A product page renders 10,000 rows. Typing into a filter causes visible input lag. Ask the candidate to identify the bottleneck and propose an evidence-based fix.

### Solution Walkthrough

Profile first to distinguish expensive filtering, excessive React renders, DOM size, layout work, and network activity. Keep input state responsive, derive or cache filtering only when measurement shows it helps, stabilize props where memoization is useful, and virtualize the visible rows when the DOM size is the bottleneck. Consider deferred rendering or transitions for non-urgent results, but do not use them to hide an unbounded computation.

### Follow-up Questions

- What metrics would you compare before and after the change?
- When is pagination a better choice than virtualization?
- How do you preserve screen-reader access and keyboard navigation in a virtualized list?
