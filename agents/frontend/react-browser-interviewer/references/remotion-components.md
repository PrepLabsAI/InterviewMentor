# Remotion Animation Components

These optional examples illustrate frontend concepts in Remotion. They are reference material for visual explanations and are not required to run the interviewer in chat.

## Event Loop Ordering

```tsx
import { useCurrentFrame } from 'remotion';

export const EventLoopTimeline = () => {
  const step = Math.floor(useCurrentFrame() / 30);
  const stages = ['Call stack', 'Microtasks', 'Render opportunity', 'Next task'];

  return (
    <div style={{ background: '#1e1e1e', color: 'white', padding: 24, width: 640 }}>
      <h2>Browser scheduling</h2>
      {stages.map((stage, index) => (
        <div
          key={stage}
          style={{
            opacity: index <= step ? 1 : 0.35,
            padding: 12,
            marginTop: 8,
            border: '1px solid #569cd6',
          }}
        >
          {index + 1}. {stage}
        </div>
      ))}
    </div>
  );
};
```

## Accessible Dialog State

```tsx
import { useCurrentFrame } from 'remotion';

export const DialogStates = () => {
  const open = Math.floor(useCurrentFrame() / 45) % 2 === 1;

  return (
    <div style={{ background: '#f5f5f5', padding: 24, width: 640, minHeight: 240 }}>
      <button aria-expanded={open}>{open ? 'Close settings' : 'Open settings'}</button>
      {open && (
        <div role="dialog" aria-modal="true" aria-labelledby="dialog-title">
          <h2 id="dialog-title">Settings</h2>
          <p>Focus is moved inside while the dialog is open.</p>
          <button>Close</button>
        </div>
      )}
    </div>
  );
};
```
