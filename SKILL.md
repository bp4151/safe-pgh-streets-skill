---
name: pgh-bike-route-safety
description: >
  Generate a Pittsburgh bicycle route safety and construction summary from a user-uploaded GPX file
  with turn-by-turn cues. Use this skill whenever a cyclist uploads a GPX file and wants to know
  about road safety, crash history, construction zones, or obstructions along their route. Also
  trigger when the user asks about biking safety in Pittsburgh, wants a pre-ride route check, or
  mentions anything about checking their route before riding. The skill uses two MCP servers:
  Safe PGH Streets (bicycle crash data per street) and DOMI Obstruction MCP (active construction
  and road closures). Always use this skill for any GPX-based Pittsburgh bike route analysis, even
  if the user just says "check my route" or "is this safe to ride."
compatibility: "Requires two MCP servers: safe-pgh-streets (https://safe-pgh-streets-mcp.brubernator.link/mcp) and domi-obstruction (https://domi-obstruction-mcp.brubernator.link/mcp)"
---

# Pittsburgh Bike Route Safety Skill

Generate a safety and construction summary for a Pittsburgh bicycle route from a user-provided GPX file.

## Overview

This skill combines two data sources:
1. **Safe PGH Streets MCP** — Bicycle crash data from Allegheny County crash records, matched to streets on the route
2. **DOMI Obstruction MCP** — Active road construction permits and closures from the City of Pittsburgh

The output is a structured report with per-street crash ratings and a construction/obstruction summary.

---

## Step 1: Parse the GPX File

The user will provide a GPX file (as an upload or pasted XML). The GPX contains turn-by-turn cues with street names.

- Extract the ordered list of street names from the GPX waypoints/cues
- Note the sequence: these are the streets the rider will travel in order
- Keep the raw GPX content available — it will be passed directly to MCP tools

---

## Step 2: Query Both MCP Servers in Parallel

Make both calls simultaneously to minimize wait time.

### Safe PGH Streets MCP
- **Server URL**: `https://safe-pgh-streets-mcp.brubernator.link/mcp`
- Pass the GPX content to the server's route-matching tool
- It returns bicycle crash records matched to streets on the route
- Each street entry should include crash count, crash severity data, and/or a computed safety score

### DOMI Obstruction MCP
- **Server URL**: `https://domi-obstruction-mcp.brubernator.link/mcp`
- Use `match_gpx_obstructions` with the raw GPX content
- Returns active obstruction/construction permits whose geometry intersects the route
- Each result includes street name, permit dates, and closure type

---

## Step 3: Build the Safety Report

Structure the output as follows:

---

### 🚲 Pittsburgh Bike Route Safety Report

**Route**: [Start → End, derived from first/last waypoint street names]  
**Total Streets Analyzed**: [N]  
**Report Generated**: [current date]

---

### ⚠️ Active Construction & Obstructions

For each obstruction that intersects the route (from DOMI):
- **Street name** and block range (if available)
- Permit/closure type (e.g., lane closure, full closure, sidewalk work)
- Active dates (start → end)
- Brief note on what to expect (e.g., "Lane reduction", "Road closed — detour required")

If no obstructions match: state "No active construction found along this route."

---

### 📊 Per-Street Crash Safety Ratings

Present a table or ordered list of each street on the route with:

| Street | Crashes (Bicycle) | Severity | Safety Rating |
|--------|-------------------|----------|---------------|
| Penn Ave | 12 | 2 fatal, 4 injury | 3/10 |
| Liberty Ave | 3 | 0 fatal, 3 injury | 7/10 |
| ... | | | |

**Safety Rating Scale (1–10)**:
- Derive from crash data returned by Safe PGH Streets
- If the server returns a pre-computed score, use it directly
- If raw crash counts are returned, apply this heuristic:
  - 9–10: 0 crashes
  - 7–8: 1–2 crashes, minor injury only
  - 5–6: 3–5 crashes OR any serious injury
  - 3–4: 6–10 crashes OR any fatality
  - 1–2: 11+ crashes OR multiple fatalities
- Round to nearest integer; never go below 1 or above 10

---

### 📝 Route Summary

A 3–5 sentence narrative summarizing:
- The overall safety character of the route (e.g., "This route has a mix of low-risk residential streets and higher-risk arterials")
- The highest-risk streets to watch out for, and why
- Any construction that significantly affects the ride
- A closing note on overall rideability

---

### 🏆 Overall Route Rating

Compute the average of all per-street Safety Ratings (weighted equally).  
Display as: **Overall Route Safety: X.X / 10** — [label]

Label thresholds:
- 8–10: ✅ Generally Safe
- 6–7.9: ⚠️ Moderate Risk — ride with care
- 4–5.9: 🔶 Higher Risk — consider alternatives
- 1–3.9: 🔴 High Risk — significant hazard history

---

## Step 4: Handling Missing or Partial Data

- If a street in the GPX has **no crash data**, list it in the table with "No data" and omit from the average
- If the **Safe PGH Streets MCP is unreachable**, note this prominently and produce only the construction section
- If the **DOMI MCP is unreachable**, note this and produce only the crash section
- If the GPX has **no recognizable street names** (raw track only, no cues), inform the user that turn-by-turn cues are required for street-level matching, and ask them to export a cue-sheet GPX from their routing app (Ride with GPS, Komoot, etc.)

---

## Notes

- This skill is Pittsburgh/Allegheny County specific — crash and obstruction data covers this region only
- Crash data reflects **historical records** (not real-time); construction data is **live/active**
- Cyclists should always use their own judgment; this report is an informational aid, not a guarantee of safety
