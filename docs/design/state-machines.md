# Run and artifact state machines

```mermaid
stateDiagram-v2
    [*] --> LOADED
    LOADED --> PAUSED
    PAUSED --> RUNNING: play
    RUNNING --> PAUSED: pause at tick boundary
    PAUSED --> PAUSED: single step
    RUNNING --> FAILED: numerical or CCD limit
    PAUSED --> FAILED: invalid execution
    RUNNING --> STOPPED
    PAUSED --> STOPPED
    STOPPED --> [*]
    FAILED --> [*]
```

A UI label cannot turn a failed run or incomplete artifact into a completed result. Every action carries current run/build/profile identity. Restart/restore uses the documented boundary rather than guessing old handles or silently replacing the artifact.

Pause/step acts at tick boundaries; render interpolation is observational. Failed numerical state has an explicit tick and pair/joint.
