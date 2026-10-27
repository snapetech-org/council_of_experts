# Confirmed-Finding Sibling Search

When a finding is confirmed, the same failure mode may exist at related call sites. Check those locations as part of the fix so a narrow repair does not leave the same confirmed issue elsewhere.

## Rule

Before a finding is marked **Fixed**, the person closing it must:

1. Identify the **fix shape**: the validator name, guard call, or invariant that resolves the original finding (e.g. `ProtocolCountReader.ReadValidatedCount`, `MessageFrameValidator.ValidateMessageLength`, an immutable-snapshot copy in a constructor).
2. Run a sibling search across the codebase for the **call shape that the original bug had**, not the fix shape. If the bug was `new byte[reader.ReadInteger()]`, the sibling search is `rg "new byte\[[^]]*Read(Integer|Long)"`.
3. For every hit, record one of:
   - **Same shape, fixed** — record the file:line and confirm the fix is in place.
   - **Same shape, also affected** — record the related location as a separate finding.
   - **Different shape, N/A** — write a one-line reason the hit doesn't apply (different boundary, already trusted input, etc.).
4. Only after all sibling hits are accounted for can the row be marked Fixed.

## Output format

The closing rationale on the original row gets a `Sibling search:` line:

```
Sibling search: rg "new byte\[[^]]*ReadInteger" src/Messaging
  src/Messaging/Foo.cs:42 — fixed (this row)
  src/Messaging/Bar.cs:88 — fixed (RT-074, prior sweep)
  src/Messaging/Baz.cs:113 — N/A, length already validated by frame guard
  src/Messaging/Qux.cs:201 — opened RT-117
```

This records the specific follow-up search and its results alongside the confirmed finding.

## When the search is too noisy to enumerate

If the targeted search produces many hits, narrow it with the originating file's directory or additional context. Review the hits relevant to the confirmed failure mode and record the affected locations.

## Interaction with the negative-space gate

The negative-space gate (`docs/dev/bug-council-negative-space.md`) declares known trust boundaries and the validator each must run. The sibling search complements it by checking related locations for the specific failure mode being fixed. Use both where they apply.

## Why this rule exists

This rule was added after a previous fix addressed one untrusted-scalar emission site but missed related locations. A targeted search during the fix would have caught those cases sooner.
