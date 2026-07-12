# The ladder method

Teach the subject by building a ladder: a numbered sequence of single-sentence statements where each rung adds exactly one new idea that rests on the rungs below it. The reader climbs one step at a time, never having to hold too much in their head at once, and never having to jump ahead to understand the step they are on.

## The format

The body is the scaffold's `<ol class="ladder">`. Each rung is one `<li class="rung">`; the number is automatic, starting at 1. A rung is just the text (and any code or figure) inside its `<li>`.

```
1. First idea. Depends on nothing but everyday knowledge.
2. Second idea. Uses only what rung 1 established.
3. Third idea. Uses only rungs 1 and 2.
...
```

## What makes a good rung

Three properties, and every rung should have all three:

**Bite-sized.** One idea per rung, in exactly one sentence. A rung that runs to a second sentence, or splices in a second idea with "and," "because," or a semicolon, is two rungs. The reader should be able to fully absorb a rung before moving to the next.

**Self-contained.** A rung is a complete, standalone thought. The reader can pause after any number and walk away with one clean idea, not a fragment that only makes sense once they read further. Never refer forward to something you have not established yet (saying "we will see why later" defeats the purpose). When you refer back, a light pointer like "(from rung 2)" is fine, but the current rung should still read as a whole thought.

**Building.** Each rung depends only on rungs that came before it, and ideally on the one or two just before it. The first rung assumes nothing but common knowledge. By the last rung, the reader has been carried the whole way without any unexplained leaps.

## Ordering principles

- **Start from the floor.** Rung 1 should be something the reader almost certainly already knows or can grasp instantly. Find the true prerequisite and begin there.
- **Introduce a term before you use it.** When a concept needs a piece of jargon, give that term its own rung (or define it inline the first time) before any later rung leans on it. No forward references.
- **One leap at a time.** If moving from one rung to the next feels like it requires the reader to figure something out themselves, insert the missing rung. The gap between consecutive rungs should be small enough to feel obvious in hindsight.
- **Land the concept.** The last rung should state the thing the user actually asked about, now fully earned by everything above it. The page has no lede and no up-front summary, so the bottom rung is where the payoff arrives.

## Length

Scale the number of rungs to the concept, and no more. A simple idea might take 4 to 6 rungs; a meatier one might need more. Do not pad with filler rungs to seem thorough, and do not cram multiple ideas into one rung to seem concise. The right length is however many small, honest steps it takes to get from the floor to the concept.

## Rest markers

The reader paces themselves by scrolling, so there is no pause-and-wait handoff. On a long ladder, give the reader periodic consolidation instead: roughly every ten rungs, drop a `<li class="rest">` that recaps the ground covered so far in one or two sentences. It takes no number and does not break the climb.

- Place a rest marker near a clean resting point, around every tenth rung. A short ladder (under about ten rungs) needs none.
- Let the final rest marker double as the closing recap on a long ladder. Do not add a separate "in short" line, and do not group rungs under section headers: the numbered climb stays continuous from rung 1 to the end.

## When a rung needs a picture

Some rungs describe things that are genuinely hard to hold in the mind from words alone: a spatial arrangement, a shape, a structure with several parts, a flow with branches or loops, how pieces fit together in space. For these, a sentence can be perfectly accurate and still leave the reader doing the hard work of assembling the picture in their head. That is exactly the kind of hidden leap the ladder exists to remove (see "one leap at a time"). A diagram closes it by letting the reader see the thing the words are pointing at.

So when you hit a rung like that, draw it: a small, clean inline `<svg>` inside a `<figure>`, placed in the rung where it first earns its place.

A picture earns its spot only when it does work that words cannot do efficiently. Reach for one when a rung involves:

- **Geometry, layout, or physical structure** (a crystal lattice, an orbital, a folded protein, a circuit). A diagram of "less dense things float" adds nothing; a diagram of the hexagonal ice lattice adds a lot.
- **A process with shape**: steps, branches, cycles, or feedback that reads more clearly as a flow than as a paragraph.
- **Several parts in relation**: a hierarchy, a network, a before-and-after, anything where the spatial arrangement is the idea.

If you cannot say what the picture would show that the sentence does not, that is the signal not to draw it.

**One diagram can serve several rungs.** Do not make a separate picture for every rung. Usually a small cluster of rungs builds toward, or leans on, the same mental image. Make one diagram for that whole cluster, place it in the rung where the picture first becomes worth showing, and let the neighboring rungs point to it ("see the diagram above"). Aim for fewer, better pictures, not one per step.

A few practical notes:

- Keep diagrams simple and uncluttered, and label them in the same plain language as the rungs. A diagram that needs its own paragraph of explanation is not pulling its weight.
- The diagram supports the rungs; it never replaces them. The ladder should still read as a complete climb with every picture removed.

## Worked example

Subject: "Why does ice float?"

1. Density is how much mass is packed into a given amount of space.
2. The same substance is denser when its particles sit closer together.
3. An object floats when it is less dense than the liquid around it.
4. So the whole question reduces to one thing: is solid ice less dense than liquid water?
5. Most substances are denser as solids than as liquids.
6. That is because cooling slows the particles until they pack tightly together.

   (Resting point: whether ice floats comes down to density alone, and most substances would sink in their own liquid.)

7. Water molecules can link to their neighbors with bonds called hydrogen bonds.
8. Hydrogen bonds only form at specific angles.
9. As water freezes, those angled bonds lock the molecules into an open, hexagonal structure.
10. That open structure holds the molecules farther apart than they sit in liquid water.
11. Held farther apart, the same molecules take up more room as ice than they did as liquid water.
12. Taking up more room with the same mass means ice is less dense than liquid water (rung 1).
13. Being less dense than the water around it, ice floats (rung 3).

Notice: rung 1 assumes only everyday knowledge, every term is defined before it is used, each rung is a single sentence carrying a single idea, and the last rung lands exactly on the question that was asked.

Rungs 6 and 9 through 12 all hinge on one mental image: how the molecules are packed in liquid water versus in solid ice. A single side-by-side diagram of the tight liquid arrangement next to the open hexagonal ice lattice, placed in rung 9 where that structure is introduced, would let the reader see the spacing rather than imagine it, and the neighboring rungs could all lean on that one image. The other rungs are abstract enough that they need no picture.
