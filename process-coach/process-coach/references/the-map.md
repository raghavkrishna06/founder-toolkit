# The map — drawing the swimlane

Read this when you are ready to draw or redraw the map. The *discipline* — one representation held all session, hand it back for correction, redraw only on material change, the hand-over keeps the full picture — is in `SKILL.md`. This file is the *how*: the layout, the legend, the arrows, and a template to copy and fill rather than building from scratch.

## The layout

For a **multi-actor** process (the usual case), draw a **horizontal swimlane**:
- One **lane** — a horizontal row — per actor, labelled with that actor's role in the founder's own words.
- The flow runs **left → right** across the **stages** of the work (the columns).
- Each step sits in the lane of whoever owns it.
- A step nobody owns goes in a **"No clear owner"** lane, so the gap shows as a box in no actor's lane.
- **Arrows** connect the steps in sequence, including the **cross-lane** arrows — those crossings between lanes are the handoffs, and handoffs are where work drops, so the arrows are what make the breaks legible, not just the boxes.

Render it as a **self-contained HTML diagram** (on a surface with artifacts, publish it as one). **Do not use Mermaid** — Mermaid has no real swimlane; its `subgraph`s only stack grouped boxes in a column, which reads as a tangle.

For a genuinely **single-actor** process, a simple vertical flow (a Mermaid `flowchart` is fine) is clearer than a one-lane swimlane. Hold whichever you pick for the whole session.

## The legend — use it exactly, on every version

Boxes:
- **neutral** (plain, grey border) — a step with a clear owner and a trigger;
- **weak joint** (solid red) — a step that exists but has no clear owner, no trigger, or no finish line;
- **missing / no owner** (dashed red) — a step that should exist but doesn't, or a handoff nobody owns;
- **today's fix** (solid green) — only on the hand-over map (see below).

Arrows:
- **solid grey arrow** — a clean handoff from one step to the next;
- **dashed red arrow** — a handoff that drops, or an arrow into a missing / unowned step.

## The arrows — how they're drawn

The arrows live in an **SVG layer over the grid**, drawn by a small script so they stay aligned to the boxes as the map grows (don't place coordinates by hand). Give every step box an `id`. After the page loads, the script reads a list of edges — each `[from-id, to-id, broken?]` — measures both boxes with `getBoundingClientRect`, and draws a line from the border of one box to the border of the next with an arrowhead. A compact edge-point helper (the point where the centre-to-centre line meets a box's border) handles arrows in any direction — across lanes as well as along one. Solid grey for a clean handoff; dashed red (`broken` = 1) for one that drops.

## The hand-over map

The final map the founder keeps must be the **full diagnostic picture, not a tidied one**: the same lanes, every **parked weak joint still red**, and the **chosen fix in green** (the `fixed` class) alongside them — so they leave with the map they learned to read, with the problems they agreed to revisit still visible. Add the green "today's fix" swatch to the legend, and make sure every legend entry matches what's actually drawn.

Hand it over as a **downloadable file** (save the HTML, or screenshot/export it) so they can keep, print and share it.

## Template — copy this, then fill in the lanes, boxes and edges

Replace the stage headers, the lanes, and the `edges` list with the founder's own process. Keep the CSS and the script as-is. The `fixed` (green) class and its swatch are only used on the hand-over map.

```html
<!doctype html>
<html lang="en"><head><meta charset="utf-8">
<style>
  :root{--ink:#1a1a1a;--line:#cfcfcf;--neutral-bg:#f4f4f5;--neutral-bd:#9ca3af;
        --red:#d42c2c;--red-bg:#fbeaea;--green:#1f8a4c;--green-bg:#e7f6ec;--lane:#fafafa;--arrow:#6b7280;}
  *{box-sizing:border-box}
  body{margin:0;background:#fff;color:var(--ink);font:14px/1.4 -apple-system,Segoe UI,Roboto,Arial,sans-serif;padding:16px}
  h1{font-size:16px;margin:0 0 4px}.sub{color:#666;margin:0 0 14px;font-size:12.5px}
  .frame{position:relative}
  /* grid: 1 label column + one column per stage. Change the "7" to your number of stages. */
  .grid{display:grid;grid-template-columns:150px repeat(7,minmax(104px,1fr));gap:8px;position:relative;z-index:1;min-width:880px}
  .wrap{overflow-x:auto}
  .stage{font-size:11px;font-weight:600;color:#555;text-align:center;padding:4px 2px;border-bottom:2px solid var(--line)}
  .lane-label{display:flex;align-items:center;font-weight:600;font-size:12.5px;background:var(--lane);border-radius:6px;padding:6px 8px}
  .cell{min-height:58px;display:flex;align-items:center;justify-content:center;padding:3px}
  .box{width:100%;min-height:48px;display:flex;align-items:center;justify-content:center;text-align:center;font-size:11px;border-radius:7px;padding:6px}
  .neutral{background:var(--neutral-bg);border:1.5px solid var(--neutral-bd)}
  .weak{background:var(--red-bg);border:2px solid var(--red);color:#7a1414;font-weight:600}
  .missing{background:#fff;border:2px dashed var(--red);color:var(--red);font-weight:600}
  .fixed{background:var(--green-bg);border:2px solid var(--green);color:#135c33;font-weight:600}
  svg.arrows{position:absolute;inset:0;width:100%;height:100%;z-index:0;pointer-events:none;overflow:visible}
  .legend{display:flex;flex-wrap:wrap;gap:16px;margin-top:16px;font-size:12px;align-items:center}
  .swatch{display:inline-block;width:24px;height:15px;border-radius:4px;vertical-align:middle;margin-right:6px}
  .s-neutral{background:var(--neutral-bg);border:1.5px solid var(--neutral-bd)}.s-weak{background:var(--red-bg);border:2px solid var(--red)}
  .s-missing{background:#fff;border:2px dashed var(--red)}.s-fixed{background:var(--green-bg);border:2px solid var(--green)}
  .lk{display:inline-block;width:26px;height:0;border-top:2px solid var(--arrow);vertical-align:middle;margin-right:6px}.lk.broken{border-top:2px dashed var(--red)}
</style></head><body>
<h1><!-- Process name --> — how it runs today (as-is)</h1>
<p class="sub">Goal: <!-- the founder's checkable goal -->. &nbsp;|&nbsp; Each row is one actor; flow runs left&rarr;right.</p>
<div class="wrap"><div class="frame">
  <svg class="arrows"><defs>
    <marker id="ah" markerWidth="9" markerHeight="9" refX="7" refY="4.5" orient="auto"><path d="M0,0 L9,4.5 L0,9 z" fill="#6b7280"/></marker>
    <marker id="ahr" markerWidth="9" markerHeight="9" refX="7" refY="4.5" orient="auto"><path d="M0,0 L9,4.5 L0,9 z" fill="#d42c2c"/></marker>
  </defs></svg>
  <div class="grid">
    <!-- header row: one empty cell, then one .stage per column -->
    <div></div>
    <div class="stage">1 · Stage</div><div class="stage">2 · Stage</div><div class="stage">3 · Stage</div>
    <div class="stage">4 · Stage</div><div class="stage">5 · Stage</div><div class="stage">6 · Stage</div><div class="stage">7 · Stage</div>

    <!-- One lane per actor: a .lane-label, then one .cell per stage column.
         Put a .box in the cell where that actor acts; leave others empty. Give each box an id. -->
    <div class="lane-label">Actor A</div>
    <div class="cell"><div class="box neutral" id="s1">First step</div></div>
    <div class="cell"></div><div class="cell"></div><div class="cell"></div><div class="cell"></div><div class="cell"></div><div class="cell"></div>

    <div class="lane-label">Actor B</div>
    <div class="cell"></div>
    <div class="cell"><div class="box weak" id="s2">A weak step</div></div>
    <div class="cell"></div><div class="cell"></div><div class="cell"></div><div class="cell"></div><div class="cell"></div>

    <div class="lane-label">No clear owner</div>
    <div class="cell"></div><div class="cell"></div>
    <div class="cell"><div class="box missing" id="s3">A step nobody owns</div></div>
    <div class="cell"></div><div class="cell"></div><div class="cell"></div><div class="cell"></div>
  </div>
</div></div>
<div class="legend">
  <span><span class="swatch s-neutral"></span>Clear owner &amp; trigger</span>
  <span><span class="swatch s-weak"></span>Weak joint</span>
  <span><span class="swatch s-missing"></span>Missing step / no owner</span>
  <!-- add on the hand-over map only: --><span><span class="swatch s-fixed"></span>Today's fix — now owned</span>
  <span><span class="lk"></span>Clean handoff</span>
  <span><span class="lk broken"></span>Handoff that drops</span>
</div>
<script>
  // edges: [from-id, to-id, broken?]  (broken = 1 draws a dashed red arrow)
  var edges=[["s1","s2",0],["s2","s3",1]];
  function draw(){
    var svg=document.querySelector('svg.arrows'), frame=document.querySelector('.frame'), fb=frame.getBoundingClientRect();
    function rc(id){var r=document.getElementById(id).getBoundingClientRect();
      return {w:r.width,h:r.height,cx:r.left-fb.left+r.width/2,cy:r.top-fb.top+r.height/2};}
    function edgePt(b,tx,ty){var dx=tx-b.cx,dy=ty-b.cy;if(!dx&&!dy)return{x:b.cx,y:b.cy};
      var sx=dx?(b.w/2)/Math.abs(dx):1e9, sy=dy?(b.h/2)/Math.abs(dy):1e9, s=Math.min(sx,sy);
      return {x:b.cx+dx*s+Math.sign(dx)*2, y:b.cy+dy*s+Math.sign(dy)*2};}
    edges.forEach(function(e){
      var a=rc(e[0]), b=rc(e[1]), p1=edgePt(a,b.cx,b.cy), p2=edgePt(b,a.cx,a.cy);
      var ln=document.createElementNS('http://www.w3.org/2000/svg','path');
      ln.setAttribute('d','M'+p1.x+','+p1.y+' L'+p2.x+','+p2.y);
      ln.setAttribute('fill','none');
      ln.setAttribute('stroke', e[2]?'#d42c2c':'#6b7280');
      ln.setAttribute('stroke-width', e[2]?'2':'1.8');
      if(e[2]) ln.setAttribute('stroke-dasharray','5,4');
      ln.setAttribute('marker-end', e[2]?'url(#ahr)':'url(#ah)');
      svg.appendChild(ln);
    });
  }
  window.addEventListener('load',draw);
</script>
</body></html>
```

On the **hand-over map**, change this file's title to the hand-over, flip the chosen fix's box(es) to `class="box fixed"` (green), leave every parked weak joint on its `weak` / `missing` class (still red), and keep the green swatch in the legend.
