---
name: genero-kickoff-to-design
description: Bootstrap a Genero website project on the Claude-only track. Builds a Claude Design canvas with a "Kickoff / Workshop" page (brief, users, journeys, sitemap, page-type wireframes, open questions) and, once the workshop is done, a "Design" page (GDS token board, shared header/footer, one template per page type, one artboard per sitemap page). Use when someone says "start a new project", "kickoff board", "workshop board", "bootstrap the design", or "move the workshop to design".
---

# Kickoff → Design on one Claude Design canvas

Reference build: Saaristo Sauna example board (ask Jonatan for the link). One canvas, two pages:
**Kickoff / Workshop** and **Design**. The client comments on the canvas; nothing goes via Miro or Figma.

## Inputs to ask for (only what is missing)

- Client name, what they sell, who decides.
- Kickoff notes or a transcript (goals, target groups, current site URL).

Don't ask about themes, tokens or code: the design is always based on GDS in generoi/bedrock, and the
person running this is often not a developer. Never invent facts. Anything unknown becomes a `[PLACEHOLDER]` or an orange sticky note.

## Phase 1: Kickoff / Workshop page

Create the canvas from the Design artifact type, title "<Client> Kickoff / Workshop". Add
`pages: [{"id":"kickoff","name":"Kickoff / Workshop"},{"id":"design","name":"Design"}]`.
Build these artboards (fixed size, static), in rows with a `title1` note above each row:

| Row | Artboard | Content |
|---|---|---|
| Strategy & users | `Main.dc.html` Kickoff (880×620) | Goal in one sentence, 3 KPIs as before → after, scope, track |
| | `Users.dc.html` (1300×620) | 3 personas: quote, needs, top task, page they land on, what holds them back |
| | sticky notes (orange) | Open questions for the client, one per note |
| Journeys & structure | `Journeys.dc.html` (1300×560) | Swimlane: persona × 4 stages, each step = action + URL + confidence bar, pain points marked |
| | `Sitemap.dc.html` (1240×~770) | Real diagram (positioned cards + arrow svgs, see the type's diagrams.md). Every page has exactly one page type |
| Page types | `WF-<Type>.dc.html` (360×900 each) | Low-fi mobile wireframe per page type, sections top to bottom with the content each carries |

Rules:
- Page types are the contract with design and dev. Keep them few; a new type needs a reason.
- Write in the client's language for page names and copy; board labels can be English.
- Run the workshop on this page: client and team comment directly. Resolve stickies before Phase 2.

## Phase 2: Design page (after the workshop)

All artboards get `"page": "design"` and live under `project/design/`.

1. **Tokens board first** (`design/Tokens.dc.html`, 1280×1500). Read
   `web/app/themes/gds/resources/styles/config/variables.scss` in generoi/bedrock and map the brand to the
   EXISTING `--gds-*` properties only: colors (primary, secondary, black, white, the four grays, success,
   error), `--gds-heading-font-family`, `--gds-text-font-family`, heading xxl→xs and text l→xs sizes
   (mobile → desktop, as `sloped-size()`), radii small/medium/large, buttons. Show GDS default next to the
   new value, and end with the `:root { … }` override block for the child theme. No new tokens.
2. **Shared parts**: `design/Header.dc.html` (prop `active` highlights the nav item, nav items are
   `<a href="<Page>.dc.html">` so Play navigates) and `design/Footer.dc.html`.
3. **One template per repeated page type** (e.g. `design/ServiceType.dc.html`) that takes a `data` prop and
   renders placeholders when it has none. Pages of that type are tiny files that only
   `<dc-import name="ServiceType" data="{{data}}">` with their own content.
4. **One artboard per sitemap page**: fluid PAGE (`"expand":"fill"`, `"is_interactive":true`), imports
   Header/Footer, uses only token values from step 1 (radius 24 on cards and buttons, 32 on hero media).
   Images are labelled placeholders `[KUVA: …]`. Lay pages out in rows of four under `title1` notes.
5. Build each section so it maps to a GDS block (media-text, media-card, post-teaser listing, process,
   accordion, cover…). Name the block in your reply, not on the artboard.

## Phase 3: Hand-off to Claude Code

- Tokens board `:root` block → the child theme's variables override.
- Page types → block patterns; templates → the same pattern filled per page.
- Content and sitemap from the canvas → pages in WordPress.

## Sharing

The canvas is private until shared from its Share menu. Live cursors and editing work for people signed in
to the Genero org or invited by email, not for public-link visitors. For live client workshops with many
participants use FigJam instead.
