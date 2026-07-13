# Document 0 – Video Production Methodology

## Purpose

Define the workflow for transforming the existing Integration Guide into an AI-assisted 60-minute engineering training video. The Integration Guide remains the technical source of truth.

This methodology document is the working contract for how we collaborate. It defines document roles, editing rules, scene format, and iteration behavior. It is not intended to become final video content.

## Deliverables

- Document 0 – Methodology
- Document 2 – Video Production Script (master working document)
- Document 3 – Production Assets & Parking Lot
- Document 1 – Optional future training manual (out of scope for now)

Document 2 is the main deliverable for the current phase. Document 3 holds reusable production material and unresolved questions. Document 1 may become an output later, but the current task is not to rewrite the Integration Guide.

## Working Rules

- Work scene-by-scene.
- Freeze structure before polishing narration.
- Keep scene numbering stable.
- Record open questions in Document 3.
- Never change technical content without asking.
- Never change the Integration Guide.

The source guide remains authoritative. The video script may reorder the guide for flow, but it must not change the solution, invent product behavior, or contradict the validated integration.

## Iterations

- Fetch the files from the repo upon explicit request.
- When an `mpe-qa` tag appears, it indicates a question from Mario and should be answered directly in the same document near the tag.
- For this phase, produce practical working versions quickly rather than over-optimizing the process.
- GitHub is used to synchronize working files; manual upload or replacement is acceptable when connector write-back is unavailable.

## Editing Philosophy

The project objective is to get to a usable video script quickly. The structure should be good enough to show to sales and marketing early, then refined only where the structure, timing, or technical credibility requires it.

The script is not a screenplay written for actors. It is an AI video production input document: clear enough for a human reviewer, structured enough for tools such as Descript or Wondershare, and technical enough for engineers.

## Scene Format

Each scene in Document 2 should eventually use the following structure. During structure freeze, not every field needs to be final, but the format should remain stable.

**Scene ID**  
Stable scene number. Do not renumber casually once structure is agreed.

**Status**  
Outline / Draft / Ready for Review / Ready for Recording / Final.

**Estimated Duration**  
Target runtime for this scene.

**Scene Purpose**  
What this scene must achieve in the viewer's mind.

**Narrative Intent**  
What the voiceover should communicate, without becoming final word-for-word narration too early.

**Visual Plan**  
What should appear on screen: animation, diagram, product GUI, screen recording, CLI, screenshot, or text overlay.

**On-Screen Actions**  
Concrete clicks, screen recordings, commands, or movements, if applicable.

**Callouts**  
Highlights, zooms, labels, arrows, warnings, or emphasis markers.

**Draft Narration**  
A first complete spoken version. This can later be refined for Descript, Wondershare, or another production tool.

**Production Notes**  
Anything that helps the editor or reviewer: pacing, dependencies, things to confirm, assets needed, or alternative takes.

**Exit / Transition**  
How the scene hands off to the next scene.

