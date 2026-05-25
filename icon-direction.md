# HitMeHuman App Icon — Design Direction Brief

## Why we're revisiting

The current icon (white card with green smiling Ace-of-Spades face on a
gradient background) was an improvement over the prior 4-suit grid, but
testers and Taylor have flagged that at small home-screen sizes:

- The face reads as a **clown / joker** more than a card trainer.
- Two "A" markers in opposite corners + the face crowds the **29pt** and
  **40pt** displays (notifications, Spotlight, Settings).
- The silhouette is **busy and asymmetric** — it gets visually lost next
  to clean app icons like Things, Bear, or Apple's own.

The goal: an icon that reads as **"serious blackjack trainer"** at a
glance, holds up at 29pt, and conveys craft without being precious.

## Design principles for this category

Reference apps that get it right in the "trainer / educational game"
space:

| App | What works |
|---|---|
| Chess.com | Single chess piece silhouette, high contrast, instantly readable |
| Lichess | Minimal knight silhouette, sharp at small sizes |
| Lumosity | Brain mark + brand color, no text |
| Elevate | Single rising-bar mark, mono palette |
| Anki / RemNote | Minimal card metaphor, no facial features |
| 21 Pro Blackjack Trainer | Clean ace + chip, no decorative noise |

Common traits:
1. **One subject, one focal point.** No multi-element compositions.
2. **No text or numerals** at the icon level — those vanish below 60pt.
3. **Hold up in monochrome** (Spotlight tinting, Apple Watch).
4. **Distinctive silhouette** that survives the rounded-rect mask.

## Four directions to explore

### Direction A — Single-glyph minimalist

A single, oversized ♠ on the jade gradient. No face, no rank, no other
shapes. Like Things 3 (single checkbox) or Bear (single bear silhouette).

**Pros:**
- Strongest possible silhouette
- Reads instantly at 29pt
- Already on-brand (jade is our primary color)
- Easy to design well — minimal craft requirements

**Cons:**
- Generic — many blackjack apps already use a single spade
- Doesn't communicate "training" vs "play"

**Reference look:** Lichess knight, but a spade.

### Direction B — "21" as the focal point

A single playing card slightly tilted, with a stylized "21" filling the
face. Two A's and a J would be conceptually correct (blackjack from
Ace+Jack) but "21" reads at every size.

**Pros:**
- Communicates blackjack concretely without a face
- Number works for international audiences (no English required)
- Distinctive — few competitors use this

**Cons:**
- Numerals at icon scale are notoriously hard; "21" must be crafted for
  the small sizes (Spotlight) where it would otherwise compress to a
  blur
- Less "warm" than a character mark

**Reference look:** Reeder's stylized R, Solitaire-Pro's "K" card.

### Direction C — Casino-chic premium

A leather-card-table green texture (matte, slightly noisy) with a
single ♠ embossed/debossed. Optional metallic gold accent line.

**Pros:**
- Premium, paid-app aesthetic
- Aligns with the Glass design system already in-app
- Differentiates from the casual / cartoon blackjack apps

**Cons:**
- Texture work needs a real designer; can look cheap if simulated
- Less playful than the current direction (a Taylor design choice)

**Reference look:** Calm's gradient panels, Apollo for Reddit's icon
treatment, Spark Email.

### Direction D — Personality with restraint

Keep the smiling Ace concept (Taylor's apparent preference) but:
- Drop both corner "A" markers (only one card showing, no pair-flip needed)
- Larger, simpler face (just eyes + smile, no spade-shaped eye details)
- Stronger card outline / shadow
- Center the face

Essentially: take what we have, simplify until it reads at 29pt.

**Pros:**
- Preserves the existing brand personality
- Smallest creative-pivot cost
- Differentiates from generic spade marks

**Cons:**
- Still risks reading as "joker" if face is too expressive
- Hardest direction to nail without a real illustrator

**Reference look:** Toca Boca's characters, Pocket's pocket icon, Bear's
bear.

## Recommendation

Start with **A + D in parallel** — they're cheap to prototype and they
cover the two viable strategic ends (pure minimal mark vs character
mark). Pick whichever survives the 29pt squint test better.

Skip B (numerals are a rabbit hole) and C (premium aesthetic requires
designer-time we don't have right now).

## Deliverables expected from a designer

For each direction:
- One 1024×1024 PNG (opaque, no alpha — Apple rejects transparent
  marketing icons)
- An optional dark-variant 1024 PNG for iOS 18+ tinted appearances
- A "screen test" composite showing the icon at 29pt, 60pt, 120pt on
  both light and dark home-screen backgrounds
- Source file (Sketch / Figma / Affinity) so we can tweak

## Constraints to respect

- **Don't reuse the SF Symbol `suit.spade.fill` as the rendered output.**
  Use it as a starting silhouette only — final mark must be custom
  vector.
- **Must remain on-brand:** primary color is jade (`#1D6F4A`) per
  `AppTheme.accent`. Keep at least one element in that family.
- **Must work alongside the in-app Glass design system** (Inter font,
  parchment surface, soft shadows).
- **Opaque only.** Apple's "Invalid large app icon. The large app icon
  in the asset catalog... can't be transparent" rejection is real and
  cost us TestFlight roundtrips during the last shipping window.
- **Light + dark variants** for the universal/single-image asset catalog
  format (already in place — `AppIcon-1024-Light.png` +
  `AppIcon-1024-Dark.png`).

## When to ship

This is **not blocking** any user-facing feature. Ship when a direction
is ready. The current smiling-Ace icon is acceptable interim until then.

---

*Audience: a designer or image-gen tool prompt. Hand this brief over,
get back 3-5 candidate 1024 PNGs per direction, pick one, drop in.*
