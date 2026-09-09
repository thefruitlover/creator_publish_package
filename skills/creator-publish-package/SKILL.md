---
name: creator-publish-package
description: Create a platform-native publishing package for any user-selected combination of YouTube, Bilibili, and REDnote from a video script supplied as a Markdown file or Notion page plus one clean base cover image. Use when a creator asks to package, publish, or adapt a video across one or more of these platforms, including titles, descriptions or posts, tags, and platform-specific covers.
---

# Creator Publish Package

Generate a complete multi-platform publishing package from a video script and clean base cover image. Understand the content once, then adapt the title, copy, and cover to each platform instead of copying or merely translating one package.

## Inputs

Require exactly two primary inputs: one script source and one cover image.

```text
script.md OR a Notion page/link
cover.png
```

Accept an optional platform selection containing any combination of `YouTube`, `Bilibili`, and `REDnote`. Generate only the selected platforms. If the user does not specify platforms, default to all three. Never require the user to select all three.

```text
Platforms: YouTube, REDnote
```

Accept the script as either a local/uploaded `script.md` file or an accessible Notion page or link. For Notion input, retrieve and read the complete page content, including relevant headings, lists, callouts, and child content that forms part of the script. If the page cannot be accessed, ask the user to connect Notion, grant access, or paste/upload the script; do not continue from a partial preview.

Treat the retrieved script content as the source of truth. It may contain Chinese, English, mixed language, headings, timestamps, or notes. Read it in full. Never invent claims, experiences, numbers, results, credentials, experiments, time periods, or conclusions unsupported by the script.

Treat `cover.png` as the visual source of truth. It may contain the creator, product UI, screenshots, a background, an existing composition, or negative space.

If either primary input is missing, ask the user to provide it before producing the package.

### Preserve portraits

If the base cover contains the creator's real face, extract the creator once from the original image as a transparent-background portrait, preserving the original face, hair, clothing, pose, and visible body pixels. Reuse this exact same portrait cutout across all selected platforms. Do not separately regenerate, redraw, beautify, relight, reshape, or reinterpret the creator for each platform.

Use generative AI only for non-person elements such as the background, product UI, supporting imagery, lighting outside the portrait, depth, and graphic accents. Assemble each final cover by deterministically compositing the shared portrait cutout onto the platform-specific generated design. This keeps the creator identical across all selected covers while allowing native layouts and backgrounds.

The transparent portrait is an internal working asset. Do not include it in the final publishing package unless the user explicitly requests it.

Allowed edits include brightness, contrast, hierarchy, text, arrows, icons, highlights, glow, shadow, simple graphics, emphasis on existing UI or screenshots, and extension or modification of non-person background areas. Keep the creator recognizable as the person in the original.

## Final output

Create `publish.md` plus one cover image for each selected platform. For example, when all three platforms are selected:

```text
publish-package/
├── publish.md
├── youtube.png
├── bilibili.png
└── rednote.png
```

Omit images for unselected platforms, and omit their sections from `publish.md`. Do not include separate title, description, tag, analysis, prompt, or metadata files unless explicitly requested. Temporary working files may be used internally but must not appear in the final package.

## Workflow

### 1. Understand the content

Read the entire script before generating titles or covers. Internally identify the main topic, target viewer, viewer payoff, strongest insight, conflict or tension, surprising realization, personal transformation, concrete supporting numbers, emotional angle, and searchable keywords. Select one strongest packaging angle. Do not output this analysis as a separate file.

### 2. Develop title and cover concepts together

Treat title and cover as a pair:

```text
Title → establishes context or promise
Cover → creates emotion, tension, or curiosity
```

Avoid repeating the same information in both. For example:

```text
Title: Vibe Coding 3周后，我对AI彻底改观了
Cover: 我高兴得太早了…
```

Develop 2–3 distinct packaging concepts and present them to the user before generating any cover images. Each concept must include:

- core packaging angle;
- a short composition description;
- the intended emotional hook or viewer payoff.

For each selected platform, provide 2–3 selectable title options and 2–3 selectable cover-text options. Mark one recommended title-cover pairing, but keep the title and cover text independently selectable. The user may choose a title from one option and cover text from another, or choose different combinations across the selected platforms.

Keep the concepts meaningfully different, such as story/transformation, practical benefit, or conflict/lesson. Present the choices compactly and identify the strongest recommended combinations, but do not generate covers yet.

Pause and ask the user to confirm:

- one packaging concept or a combination of concept elements;
- one title for each selected platform;
- one cover-text option for each selected platform.

Continue only after both title and cover text are selected for every selected platform. If the user explicitly says `auto choose`, `直接生成`, or otherwise clearly requests no approval step, select the strongest title-cover pairing for each selected platform and continue without pausing.

### 3. Adapt by platform

Do not simply translate or copy one package.

#### YouTube

Prioritize curiosity, story, transformation, tension, clear viewer payoff, and a strong title-cover pair. Keep titles concise and avoid keyword stuffing.

Create a 16:9 cover at 1280 × 720. Optimize for click-through at small size with one focal point, one supporting visual, and a short hook. Prefer 2–8 Chinese characters or 2–6 short English words; use longer text only when clearly justified. Avoid repeating the full title.

#### Bilibili

Prioritize clarity, topic specificity, useful information density, Chinese readability, and curiosity without excessive vagueness. Titles may state more explicitly what the viewer will learn.

Create a 16:9 master cover at 1280 × 720. Slightly more explanatory Chinese text is acceptable. Keep essential text, facial features, and supporting visuals inside a central safe area so they survive a tighter 4:3 crop. Do not place essential content near extreme left or right edges. Do not duplicate the YouTube image unless that design genuinely works best.

#### REDnote

Prioritize immediate relevance, personal experience, useful takeaways, emotional resonance, mobile readability, and save/share value. Use a conversational, benefit-driven title.

Create a native vertical 3:4 cover at 1080 × 1440. Recompose the base cover instead of center-cropping the 16:9 design. Preserve the portrait and use larger mobile-readable Chinese text. The result should feel intentionally designed for a vertical REDnote feed.

### 4. Create `publish.md`

Create one practical Markdown file containing only the selected platform sections, in this order when present:

```markdown
# Publish Package

## YouTube

### Recommended Title
...

### Alternative Titles
1. ...
2. ...

### Description
...

### Thumbnail Text
...

### Tags
...

---

## Bilibili

### Recommended Title
...

### Alternative Titles
1. ...
2. ...

### Description
...

### Cover Text
...

### Tags
...

---

## REDnote

### Recommended Title
...

### Alternative Titles
1. ...
2. ...

### Post
...

### Cover Text
...

### Hashtags
...
```

Do not add explanations for the selections unless requested. Make every section immediately copyable into its platform.

### 5. Write native publishing copy

For YouTube, always make both the Description and Tags bilingual in Chinese and English, even when the script is predominantly one language.

Write the Chinese description first, followed by a simple divider and a complete English description. Each language section must work independently as natural publishing copy; preserve the same supported facts and viewer promise without forcing a sentence-by-sentence literal translation. Begin each section with 1–3 sentences explaining why someone should watch, then briefly describe the content. Add a compact topic list when useful.

Include both natural Chinese search terms and natural English search terms in `### Tags`. Cover the main topic, relevant tools or products, audience intent, and close keyword variants without stuffing or duplicating meaningless translations.

Do not invent links, sponsors, affiliate links, social profiles, or calls to action.

For Bilibili, write naturally for a Chinese-speaking audience. Be slightly more explanatory than YouTube when useful and avoid robotic SEO language.

For REDnote, write a native post rather than reusing the YouTube description. Prefer a personal opening, concise paragraphs, concrete takeaways, conversational Chinese, useful keywords, restrained emoji, and restrained hashtags. Avoid exaggerated marketing language.

### 6. Create the covers

Inspect `cover.png` before editing. Determine its focal point, creator location, negative space, background complexity, existing UI or screenshots, text placement, and crop constraints.

Use the base image as the visual foundation for every selected cover. Create platform-native variants following the dimensions and composition rules above.

### Generative cover policy

Use generative AI image editing by default for the non-person portions of all selected covers. Use the supplied cover as the visual reference, while allowing the model to redesign background, product UI, supporting imagery, lighting, depth, perspective, graphic accents, and overall composition. Do not ask the model to regenerate the creator.

Generate each platform cover independently with its own prompt and composition. Do not create one horizontal image and mechanically crop it into all formats.

For each platform, generate a clean background/layout plate with suitable space for the shared portrait, then composite the exact same extracted portrait onto it. Scale and position the cutout as needed for each aspect ratio, but do not distort, mirror, repaint, or alter the portrait itself. Match the surrounding background to the portrait with restrained shadow or edge treatment without changing portrait pixels.

When the original cover has a natural creator environment, keep some visibly recognizable original background in every platform cover so the result feels natural and personal. Preserve useful elements such as the room, window, furniture, plants, wall color, or artwork instead of replacing the whole scene. Generative editing may clean, extend, simplify, or recompose the non-person background, but must not replace all of its character with a generic studio or gradient unless the user explicitly requests a completely new background.

### Portrait mask and layer integrity

Validate the shared portrait cutout before composing any final cover. The face, hair, neck, clothing, arms, hands, and visible accessories must remain opaque wherever they were visible in the source. Only pixels outside the creator may be transparent. Checkerboard pixels, background remnants, holes through the body, or partial transparency that allows the background to show through the creator are failures; regenerate or repair the mask before continuing.

Add a clean white outline around the entire outside edge of the extracted portrait by default. The outline should make the cutout feel intentional against the retained original background and remain visible at feed size, but it must not cover facial features, hair, clothing, arms, or hands. Omit the outline only when the user explicitly requests no outline.

Use this fixed back-to-front compositing order:

1. background plate;
2. supporting visual and headline;
3. white portrait outline;
4. opaque portrait cutout.

Never place a background, texture, color wash, headline panel, or supporting visual above the portrait. After compositing, inspect the face, hair, shirt, arms, and hands at full size and at thumbnail size. If any background appears to pass through or cover the creator, do not finalize the cover.

### Clean visual direction

Keep generated covers simple, clean, and immediately understandable. Default to:

- one creator or primary subject;
- one supporting visual, such as one simplified product window, one symbolic object, or one before/after comparison;
- one short headline;
- generous negative space;
- no more than two strong accent colors plus neutrals.

Avoid dense dashboards, multiple competing UI cards, repeated badges, excessive arrows, heavy neon glow, tiny interface labels, and decorative elements that do not strengthen the hook. Simplify real product interfaces into one readable visual rather than reproducing every feature or workflow stage.

The cover must communicate its idea in about one second at feed size. If removing an element does not weaken the hook, remove it.

Inspect every generated cover for facial fidelity, exact headline text, visual hierarchy, dimensions, crop safety, and unwanted artifacts. Retry a generation when the face, text, or composition is materially wrong.

Use non-generative cropping and deterministic layout only when:

- the user explicitly requests no generative editing or pixel-exact portrait preservation;
- the image-generation tool is unavailable or repeatedly rejects the supplied image;
- repeated generations cannot preserve the creator's identity or required text reliably.

When falling back, preserve the original portrait pixels and explain briefly that the cover used a non-generative composition.

Unless the user specifies another style, use a bright, clean, modern, high-contrast, visually simple, creator-focused look. Keep it professional but not corporate. Avoid unnecessary darkness, clutter, tiny text, and filling every area. Use whitespace deliberately.

## Integrity and clickbait

Use curiosity without deception. Emphasize tension only when the script supports it. A line such as `我高兴得太早了…` is appropriate only when the script genuinely describes excitement followed by problems. Never manufacture a more dramatic story than the content supports.

Infer the primary language from the script. For predominantly Chinese scripts, default to Chinese titles and copy while preserving established English technical terms such as `Vibe Coding`, `Codex`, `Claude Code`, `AI`, `ETF`, and `S&P 500` when natural.

## Quality check

Before finalizing, verify:

- Every major claim is supported by the script.
- The strongest angle is represented and titles are specific.
- Each selected platform feels native.
- When YouTube is selected, its Description contains complete Chinese and English publishing copy.
- When YouTube is selected, its Tags contain useful Chinese and English keywords.
- Each cover complements rather than repeats its title.
- The cover is understandable in about one second and readable when small.
- The user selected or approved the packaging concept, platform title, and platform cover text separately, unless they explicitly requested automatic selection.
- Each cover contains one dominant subject, one supporting visual, and one short headline rather than a dense collection of elements.
- The original creator remains recognizable and the portrait was not unnecessarily regenerated.
- All selected covers reuse the same portrait cutout from the original image; facial features, clothing, and pose are consistent.
- The portrait mask has no transparent holes or background bleed through the face, hair, clothing, arms, or hands.
- The white outline sits behind the portrait, and the complete portrait sits above every background and design layer.
- Recognizable original background elements remain when they help the cover feel natural and personal.
- The composition is bright and uncluttered.
- When Bilibili is selected, its design survives a central 4:3 crop.
- When REDnote is selected, its design is genuinely recomposed for vertical.
- The final package contains only `publish.md` and the cover images for the selected platforms unless the user requested more.

## Invocation

Support concise requests such as:

```text
Create a publish package from:
Script: [Notion page/link or ./script.md]
Cover: ./cover.png
Platforms: YouTube, REDnote
```

or:

```text
/publish [Notion page/link] ./cover.png
```

Do not require the user to restate platform strategy, dimensions, copy structure, or cover rules. If `Platforms` is omitted, generate all three platforms.
