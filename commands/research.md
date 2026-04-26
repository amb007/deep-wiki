---
description: Conduct multi-turn deep research on a specific topic with evidence-based analysis
---

# Deep Wiki: Research

Conduct systematic, multi-turn research on a specific topic. Each iteration reveals a new layer of understanding.

## Process

### Step 1: Source Repository Resolution

1. Run `git remote get-url origin` to detect remote URL
2. Ask the user if not already provided: _"Source repo URL? (or 'local' for local-only citations)"_
3. Determine branch: `git rev-parse --abbrev-ref HEAD`
4. Store citation format:
   - **Remote**: `[file:line](REPO_URL/blob/BRANCH/file#Lline)`
   - **Local**: `(file:line)`

### Step 2: Research Iterations

Conduct 5 progressive iterations:

1. **Structural Survey**: Map components, boundaries, entry points
2. **Data Flow Analysis**: Trace data through the system
3. **Integration Mapping**: External connections and protocols
4. **Pattern Recognition**: Design patterns, anti-patterns, decisions
5. **Synthesis**: Combine findings into actionable insights

### Step 3: Findings Format

For each significant finding:

1. **Finding**: One clear sentence
2. **Evidence**: File paths, code references, call chains
3. **Implication**: Why this matters for the system
4. **Confidence**: HIGH/MEDIUM/LOW
5. **Open Questions**: What needs tracing next

### Requirements

- NEVER repeat yourself — each iteration adds new insights
- ALWAYS cite specific files with line numbers
- Include Mermaid diagrams when they illuminate discoveries
- Add `<!-- Sources: ... -->` comment blocks after diagrams
- Maintain laser focus on the research topic
- Track knowledge map: Explored ✅, Partially Explored 🔶, Unexplored ❓

### Example Output

```markdown
## Research: Caching Layer

### Iteration 1: Structural Survey

**Finding**: The caching layer uses Redis with a custom wrapper class `CacheService`.
**Evidence**: [src/cache/service.ts:1](REPO_URL/blob/BRANCH/src/cache/service.ts#L1) defines `CacheService` class
**Implication**: Centralized caching abstraction for the application
**Confidence**: HIGH
**Open Questions**: What caching strategies are implemented?

```mermaid
graph LR
  A[Application] --> B[CacheService]
  B --> C[Redis]
```
<!-- Sources: src/cache/service.ts:1 -->

### Iteration 2: Data Flow Analysis

**Finding**: Cache keys follow pattern `prefix:entity:id` with TTL of 3600 seconds.
**Evidence**: [src/cache/service.ts:42-58](REPO_URL/blob/BRANCH/src/cache/service.ts#L42-L58) shows key generation
**Implication**: Consistent key structure enables cache invalidation patterns
**Confidence**: HIGH
**Open Questions**: How is cache invalidation handled?

... (continue for 5 iterations)

### Synthesis

The caching layer provides a centralized Redis interface with consistent key patterns and TTL management. Cache invalidation uses event-based triggers from database changes.

**Recommendations**:
- Document cache key patterns in README
- Add metrics for cache hit/miss ratios
- Consider adding cache warming for critical paths
```

$ARGUMENTS
