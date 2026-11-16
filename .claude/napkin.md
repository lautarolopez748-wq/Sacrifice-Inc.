# Napkin Runbook

## Curation Rules
- Re-prioritize on every read.
- Keep recurring, high-value notes only.
- Max 10 items per category.
- Each item includes date + "Do instead".

## User Directives (Highest Priority)
1. **[2026-11-16] Operator has ZERO programming/3D/Unity/Blender experience**
   Do instead: automate what can be automated; explain decisions in plain language; give exact click-path steps when manual action is needed; never assume technical vocabulary; never simplify scope just because operator is a beginner.
2. **[2026-11-16] Approval gates before work**
   Do instead: inspect project first, propose plan before modifying; never invent story/mechanics decisions and present as approved; story/mechanics require operator sign-off. GDD is source of truth and must be updated on approved changes.
3. **[2026-11-16] Git discipline**
   Do instead: commit only at functional tested milestones; never commit broken functionality; never push without operator authorizing the milestone; keep history clean.
4. **[2026-11-16] Direct, terse communication**
   Do instead: no gigantic reports; direct concrete answers; when manual steps needed: what/where/exact steps, then wait for confirmation.
5. **[2026-11-16] Hardware is a hard constraint (Pentium G4560, GTX 750 2GB, 8GB RAM, Win10)**
   Do instead: Low Poly + URP; bake lighting; small textures (mostly 512-1024); low shadow distance; test performance on this machine regularly; never design for high-end hardware.
6. **[2026-11-16] Disk discipline: never touch C:**
   Do instead: project lives on E:\Sacrifice Inc (D: denied write for this user); E: has ~900GB free. Install Unity/Blender/caches on E:, never C:.

## Project Guardrails
1. **[2026-11-16] Identity = corporate black comedy + strategic dismemberment puzzles**
   Do instead: reject turning the game into generic shooter/survival horror/jumpscare-fest/physics-sandbox; every major decision must reinforce Integrity Corp. satire and body-sacrifice mechanics. No copied assets/characters from other games.
2. **[2026-11-16] Forbidden shortcuts**
   Do instead: no temporary fixes becoming permanent architecture; no packages/frameworks without justification; official Unity tools and stable versions first; modular reusable systems only.

## Shell & Command Reliability
1. **[2026-11-16] D:\ is read-only for this user (owned by Administrators, session not elevated)**
   Do instead: work on E:\; if operator wants project on D:, they must grant Modify permission to their user on the folder or run an elevated session.
2. **[2026-11-16] Git installed but identity (user.name/user.email) NOT configured**
   Do instead: set identity with operator-approved name/email before first commit; confirm before any push.
