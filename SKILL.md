---
name: fireworks-tech-graph
description: Use when the user wants to create any technical diagram - architecture, data flow, flowchart, sequence, agent/memory, or concept map - and export as SVG+PNG. Trigger on: "画图" "帮我画" "生成图" "做个图" "架构图" "流程图" "可视化一下" "出图" "generate diagram" "draw diagram" "visualize" or any system/flow description the user wants illustrated.
---

# fireworks-tech-graph

Generate production-quality SVG technical diagrams exported as PNG via `rsvg-convert`.

## Tool Support

You do NOT have direct access to a design tool or SVG layout engine. You must:
- Generate or edit SVG/Markdown/templates directly using tools.
- Use the repo's references and templates to build diagrams.
- Validate SVG syntax before claiming success.

## When To Use

Use for:
- Architecture diagrams
- Data-flow diagrams
- Flowcharts and decision trees
- Sequence diagrams
- Agent/memory diagrams
- Concept maps / mind maps
- Comparison matrices
- UML diagrams (14 types supported)

Do NOT use for:
- Charting numeric data (bar/line/pie)
- Figma-like UI mockups
- Photorealistic images
- Low-effort ASCII art when a real diagram is expected

## Required Repo Context

Before drawing, inspect these files as needed:

1. `references/icons.md`
2. Relevant style guide(s):
   - `references/style-1-flat-icon.md`
   - `references/style-2-dark-terminal.md`
   - `references/style-3-blueprint.md`
   - `references/style-4-notion-clean.md`
   - `references/style-5-glassmorphism.md`
   - `references/style-6-claude-official.md`
   - `references/style-7-openai.md`
3. `templates/*.svg`
4. `scripts/README.md`

## Validation Tools

### 1. `generate-diagram.sh` - Validate SVG + export PNG
```bash
./scripts/generate-diagram.sh -t architecture -s 1 -o ./output/arch.svg
```
- Validates with `validate-svg.sh`
- Exports 1920px PNG via `rsvg-convert`
- Example: `./scripts/generate-diagram.sh -t architecture -s 1 -o ./output/arch.svg`

### 2. `generate-from-template.py` - Generate SVG from template + JSON
```bash
python3 ./scripts/generate-from-template.py architecture ./output/arch.svg '{"title":"My Diagram","nodes":[],"arrows":[]}'
```
- Builds an SVG directly from `templates/*.svg` and structured JSON
- Embeds style tokens, semantic node kinds, richer arrow routing, and optional containers / legend / footer chrome
- Escapes text content to keep output XML-valid

### 3. `validate-svg.sh` - Validate SVG syntax
```bash
./scripts/validate-svg.sh <svg-file>
```

## Workflow

1. **Classify the request**
   - Architecture
   - Data flow
   - Flowchart
   - Sequence
   - Agent architecture
   - Memory architecture
   - UML subtype if applicable
   - Comparison / matrix
   - Mind map

2. **Choose style**
   - Default: Style 1 (Flat Icon)
   - Dark technical: Style 2 or 3
   - Minimal doc-like: Style 4
   - Brand-specific: Style 6 or 7
   - Product keynote / polished hero: Style 5

3. **Choose output structure**
   Use the most appropriate layout:
   - Horizontal layered architecture
   - Vertical process flow
   - Swim lanes
   - Matrix grid
   - Radial map
   - UML conventions

4. **Map concepts to semantic shapes**
   - User -> human icon
   - LLM -> rounded rectangle, double border, lightning glyph
   - Agent -> hexagon
   - Memory -> dashed box / cylinder depending on type
   - Vector store -> ringed cylinder
   - Tool -> gear box
   - DB / Graph -> semantic storage shape
   - External system -> dashed rectangle

5. **Write SVG or structured input**
   - Prefer structured JSON + `generate-from-template.py` when the layout matches an existing template or regression fixture pattern. Pass node ids plus `source` / `target` in arrows so routing can anchor to real ports.
   - Use `containers` for grouped sections / swim lanes.
   - Use `nodes[].kind` for semantic shapes instead of drawing every primitive by hand.
   - When drawing manual SVG, keep everything inline with no external assets.
   - Reuse paths and tokens from `references/*.md` whenever possible.

6. **Validate syntax**
   Run:
   ```bash
   ./scripts/validate-svg.sh /path/to/file.svg
   ```

7. **Fix any issues**
   - Missing closing tags
   - Unquoted attributes
   - Invalid entities
   - Broken markers / ids

8. **Validate**: Run `rsvg-convert file.svg -o /dev/null 2>&1` to check syntax
9. **Export PNG**: `rsvg-convert -w 1920 file.svg -o file.png`
10. **Report output files**

## Diagram-Type Specific Guidance

### Architecture Diagram
Use when showing components and how they connect.

Layout:
- Prefer left-to-right or top-to-bottom layers
- Use swim lanes if tiers are important (frontend / services / storage)
- Keep crossing arrows minimal

Required elements:
- Clear title
- Labeled components
- Directional arrows
- Optional legend if arrow colors encode meaning

### Data Flow Diagram
Use when the emphasis is what data moves between systems.

Layout:
- Keep data transformations explicit
- Label arrows with payloads / events / artifacts
- Use storage icons for persistence points

### Flowchart
Use for decision logic or operational workflows.

Conventions:
- Diamond = decision
- Rectangle = action
- Rounded rectangle = start/end if appropriate
- Label edge conditions (`yes`, `no`)

### Sequence Diagram
Use for time-ordered interactions.

Conventions:
- Participants across top
- Lifelines vertical
- Messages horizontal
- Activation bars optional but helpful

### Agent / Memory Diagram
Use repo-specific shape vocabulary.

Typical patterns:
- Orchestrator / Planner agent at center or top
- Tools on one side, memory stores below or adjacent
- Distinguish read vs write arrows
- Highlight feedback loops and retrieval

### Comparison Matrix
Use for side-by-side capability comparison.

Conventions:
- Rows = criteria
- Columns = systems / approaches
- Use check icons, dots, short phrases
- Avoid overloading with paragraphs

### UML Support
All 14 UML diagram types supported. Use correct UML notation conventions:

#### Structural UML
- **Class Diagram**: Classes with compartments (name, attributes, methods), inheritance arrows, association lines
- **Component Diagram**: Components as boxes with interface lollipops/sockets, dependency arrows
- **Deployment Diagram**: Nodes as 3D boxes, artifacts inside, communication paths
- **Package Diagram**: Package tabs, dependency arrows between packages
- **Composite Structure**: Parts, ports, connectors within class/component boundary
- **Object Diagram**: Object instances with underlined names, links between objects

#### Behavioral UML
- **Use Case Diagram**: Actors as stick figures, use cases as ovals, system boundary box
- **Activity Diagram**: Initial/final nodes, action rectangles, decision diamonds, fork/join bars
- **State Machine**: States as rounded rectangles, transitions with event labels, initial/final pseudo-states
- **Sequence Diagram**: Lifelines, messages, activation boxes, combined fragments
- **Communication Diagram**: Objects + numbered messages on links
- **Timing Diagram**: Time axis horizontal, state/value changes over time
- **Interaction Overview**: Activity diagram with interaction use nodes

#### Domain-Specific
- **ER Diagram**: Entities as rectangles, relationships as diamonds/lines, cardinality labels

## Style Guide Summary

### Style 1 - Flat Icon (Default)
- White background
- Soft shadows
- Colored icon accents
- Great for docs/blogs

### Style 2 - Dark Terminal
- Dark background
- Neon accents
- Monospace labels
- Great for GitHub/dev content

### Style 3 - Blueprint
- Deep blue background
- Grid lines / blueprint feel
- Cyan strokes
- Great for architecture/engineering docs

### Style 4 - Notion Clean
- Minimal white background
- Very restrained color use
- Clean typography
- Great for internal docs

### Style 5 - Glassmorphism
- Dark gradient background
- Frosted cards
- Subtle blur-like effects in SVG
- Great for keynote / polished visuals

### Style 6 - Claude Official
- Warm cream background `#f8f6f3`
- Anthropic-inspired palette: oranges, browns, warm grays
- Clean, restrained, professional
- Great for Claude/Anthropic-adjacent system diagrams

### Style 7 - OpenAI Official
- Pure white background `#ffffff`
- OpenAI-inspired palette: greens, grays, black
- Minimal, modern, precise
- Great for OpenAI-adjacent API/architecture diagrams

## File Structure

- `references/` -> style guides + icons
- `templates/` -> reusable starter SVGs
- `scripts/` -> validation/export helpers

## Quality Bar

Every delivered diagram should be:
- Readable at a glance
- Semantically organized
- Visually consistent with the chosen style
- Free of SVG syntax errors
- Exported successfully to PNG when required

If the user gives a rough description, infer a sane structure. If the diagram could reasonably be interpreted multiple ways, pick the clearest one rather than overcomplicating it.

## Layout & Composition Rules

These rules matter more than decorative flourish.

### Architecture / AI-Agent diagrams
- Use 3 to 5 major zones max.
- Align to a grid.
- Keep primary flow obvious in one direction.
- Minimize line crossings.
- Use consistent node widths within the same layer.
- Reserve large titles and legends for the outer frame, not the core flow.

### Comparison / matrix diagrams
- Max 6 columns before readability collapses.
- Keep row labels short.
- Use subtle separators rather than heavy full-table borders.
- Highlight only the most important differences.

### Sequence / flow diagrams
- Vertical spacing should clearly communicate progression.
- Decision labels must sit near their branch arrows.
- Don’t route arrows through labels or shapes.

## Shape Vocabulary

Use these defaults unless the user explicitly asks otherwise.

| Concept | Shape | Notes |
|---|---|---|
| User / Human | human icon or circle avatar | |
| LLM / Model | rounded rect with double border + bolt | |
| Agent / Planner / Orchestrator | hexagon | |
| Short-term memory | dashed rounded rect | |
| Long-term memory | cylinder | |
| Vector store | cylinder with ring lines inside | Add 2-3 concentric ellipses |
| Graph DB | Circle cluster (3 overlapping circles) | |
| Tool / Function | Gear-like rect or rect with wrench icon | |
| API / Gateway | Hexagon (single border) | |
| Queue / Stream | Horizontal tube (pipe shape) | |
| File / Document | Folded-corner rect | |
| Browser / UI | Rect with 3-dot titlebar | |
| Decision | Diamond | Flowcharts only |
| Process / Step | Rounded rect | Standard box |
| External Service | Rect with cloud icon or dashed border | |
| Data / Artifact | Parallelogram | I/O in flowcharts |

## Arrow Semantics

Always assign arrow meaning, not just color:

| Flow Type | Color | Stroke | Dash | Meaning |
|-----------|-------|--------|------|---------|
| Primary data flow | blue `#2563eb` | 2px solid | none | Main request/response path |
| Control / trigger | orange `#ea580c` | 1.5px solid | none | One system triggering another |
| Memory read | green `#059669` | 1.5px solid | none | Retrieval from store |
| Memory write | green `#059669` | 1.5px | `5,3` | Write/store operation |
| Async / event | gray `#6b7280` | 1.5px | `4,2` | Non-blocking, event-driven |
| Embedding / transform | purple `#7c3aed` | 1px solid | none | Data transformation |
| Feedback / loop | purple `#7c3aed` | 1.5px curved | none | Iterative reasoning loop |

Always include a **legend** when 2+ arrow types are used.

## Layout Rules & Validation

**Spacing**:
- Same-layer nodes: 80px horizontal, 120px vertical between layers
- Canvas margins: 40px minimum, 60px between node edges
- Snap to 8px grid: horizontal 120px intervals, vertical 120px intervals

**Arrow Labels** (CRITICAL):
- MUST have background rect: `<rect fill="canvas_bg" opacity="0.95"/>` with 4px horizontal, 2px vertical padding
- Place mid-arrow, ≤3 words, stagger by 15-20px when multiple arrows converge
- Maintain 10px safety distance from nodes

**Arrow Routing**:
- Prefer orthogonal (L-shaped) paths to minimize crossings
- Anchor arrows on component edges, not geometric centers
- Route around dense node clusters, use different y-offsets for parallel arrows
- Jump-over arcs (5px radius) for unavoidable crossings

**Line Overlap Prevention** (CRITICAL - most common bug on Codex):
When two arrows must cross each other, ALWAYS use jump-over arcs to prevent visual overlap:
- Crossing horizontal arrows: add a small semicircle arc (radius 5px, stroke same color as arrow, fill none) that "jumps over" the other line
- SVG pattern for jump-over: use a white/matching-background arc on the lower layer, then draw the upper arc on top
- Multiple crossings: stagger arc radii (5px, 7px, 9px) so arcs don't overlap each other
- Never let two arrows' straight-line segments cross without a jump-over arc

**Validation Checklist** (run before finalizing):
1. **Arrow-Component Collision**: Arrows MUST NOT pass through component interiors (route around with orthogonal paths)
2. **Text Overflow**: All text MUST fit with 8px padding (estimate: `text.length × 7px ≤ shape_width - 16px`)
3. **Arrow-Text Alignment**: Arrow endpoints MUST connect to shape edges (not floating); all arrow labels MUST have background rects
4. **Container Discipline**: Prefer arrows entering and leaving section containers through open gaps between components, not through inner component bodies

## SVG Technical Rules

- ViewBox: `0 0 960 600` default; `0 0 960 800` tall; `0 0 1200 600` wide
- Fonts: embed via `<style>font-family: ...</style>` — no external `@import` (breaks rsvg-convert)
- `<defs>`: arrow markers, gradients, filters, clip paths
- Text: minimum 12px, prefer 13-14px labels, 11px sub-labels, 16-18px titles
- All arrows: `<marker>` with `markerEnd`, sized `markerWidth="10" markerHeight="7"`
- Drop shadows: `<feDropShadow>` in `<filter>`, apply sparingly (key nodes only)
- Curved paths: use `M x1,y1 C cx1,cy1 cx2,cy2 x2,y2` cubic bezier for loops/feedback arrows
- Clip content: use `<clipPath>` if text might overflow a node box

## SVG Generation & Error Prevention

**MANDATORY: Python List Method** (ALWAYS use this):
```python
python3 << 'EOF'
lines = []
lines.append('<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 960 700">')
lines.append('  <defs>')
# ... each line separately
lines.append('</svg>')

with open('/path/to/output.svg', 'w') as f:
    f.write('\n'.join(lines))
print("SVG generated successfully")
EOF
```

**Why mandatory**: Prevents character truncation, typos, and syntax errors. Each line is independent and easy to verify.

**Pre-Tool-Call Checklist** (CRITICAL - use EVERY time):
1. ✅ Can I write out the COMPLETE command/content right now?
2. ✅ Do I have ALL required parameters ready?
3. ✅ Have I checked for syntax errors in my prepared content?

**If ANY answer is NO**: STOP. Do NOT call the tool. Prepare the content first.

**Error Recovery Protocol**:
- **First error**: Analyze root cause, apply targeted fix
- **Second error**: Switch method entirely (Python list → chunked generation)
- **Third error**: STOP and report to user - do NOT loop endlessly
- **Never**: Retry the same failing command or call tools with empty parameters

**Validation** (run after generation):
```bash
rsvg-convert file.svg -o /tmp/test.png 2>&1 && echo "✓ Valid" && rm /tmp/test.png
```

**If using `generate-from-template.py`**:
- Prefer `source` / `target` node ids in arrow JSON so the generator can snap to node edges
- Keep `x1,y1,x2,y2` as hints or fallback coordinates, not the main routing primitive
- Let the generator choose orthogonal routes; avoid hardcoding center-to-center straight lines unless the path is guaranteed clear

**Common Syntax Errors to Avoid**:
- ❌ `yt-anchor` → ✅ `y="60" text-anchor="middle"`
- ❌ `x="390` (missing y) → ✅ `x="390" y="250"`
- ❌ `fill=#fff` → ✅ `fill="#ffffff"`
- ❌ `marker-end=` → ✅ `marker-end="url(#arrow)"`
- ❌ `L 29450` → ✅ `L 290,220`
- ❌ Missing `</svg>` at end

## Output

- **Default**: `/Users/bytedance/Downloads/[derived-name].svg` and `/Users/bytedance/Downloads/[derived-name].png`
- **Custom**: user specifies file or directory path with `--output /path/` or `输出到 /path/`
- **PNG export**: `rsvg-convert -w 1920 file.svg -o file.png` (1920px = 2x retina)

## Styles

| # | Name | Background | Best For |
|---|------|-----------|----------|
| 1 | **Flat Icon** (default) | White | Blogs, docs, presentations |
| 2 | **Dark Terminal** | `#0f0f1a` | GitHub, dev articles |
| 3 | **Blueprint** | `#0a1628` | Architecture docs |
| 4 | **Notion Clean** | White, minimal | Notionnce |
| 5 | **Glassmorphism** | Dark gradient | Product sites, keynotes |
| 6 | **Claude Official** | Warm cream `#f8f6f3` | Anthropic-style diagrams |
| 7 | **OpenAI Official** | Pure white `#ffffff` | OpenAI-style diagrams |

Load `references/style-N.md` for exact color tokens and SVG patterns.

## Style Selection

**Default**: Style 1 (Flat Icon) for most diagrams. Load `references/style-diagram-matrix.md` for detailed style-to-diagram-type recommendations.

These patterns appear frequently — internalize them:

**RAG Pipeline**: Query → Embed → VectorSearch → Retrieve → Augment → LLM → Response
**Agentic RAG**: adds Agent loop with Tool use between Query and LLM
**Agentic Search**: Query → Planner → [Search Tool / Calculator / Code] → Synthesizer → Response
**Mem0 / Memory Layer**: Input → Memory Manager → [Write: VectorDB + GraphDB] / [Read: Retrieve+Rank] → Context
**Agent Memory Types**: Sensory (raw input) → Working (context window) → Episodic (past interactions) → Semantic (facts) → Procedural (skills)
**Multi-Agent**: Orchestrator → [SubAgent A / SubAgent B / SubAgent C] → Aggregator → Output
**Tool Call Flow**: LLM → Tool Selector → Tool Execution → Result Parser → LLM (loop)
