# Why I'm building this

I didn't start out here. My first picture of AI was the common one — a
fast, capable system you hand a problem to and trust to hand back a good
answer. That picture didn't survive contact with actually building
something on top of these systems, and the correction wasn't gentle.

Fallacy detection is where it really turned for me. Studying how
arguments fail — where something reads as valid but isn't — is close to
the actual core problem with language models: fluency and correctness
come apart, and fluency is cheap to produce at scale. A model can be
wrong in a way that sounds confident and coherent the entire way down,
with nothing about its surface that flags the difference. That's not how
I understood computing before. Software used to fail loudly. This fails
quietly, and the quiet is the dangerous part.

Once that reframing happens, a few things stop being optional. Language
is a messy medium, and systems built natively on it resist the kind of
hard guarantees deterministic code can offer — which means the
conventions and gates that keep a system honest have to be built
*despite* that looseness, not assumed away by it. And problem-solving, in
the places that matter, reverts back to humans. Not as a fallback for
when the AI isn't good enough yet, but as a structural requirement,
because an autoregressive system can commit to a bad path one token at a
time, in a way that's coherent at every step and only visible as a
mistake once it's already compounded — a cascade with no clean trace back
to where it went wrong. A goal pushed hard enough in the wrong direction
doesn't just underperform; it can invert, and look like success the whole
way there.

I think too many people are still standing where I started: handing
real decisions to AI systems and hoping for the best, without the
infrastructure to notice when "the best" quietly stopped being true. That
gap — between how casually this technology gets trusted and how little
anyone can actually prove about its worst-case behavior — is where the
real damage lives. No amount of training or constitutional framing turns
that gap into a guarantee. It only narrows the odds.

Tropelex is what I built once I stopped believing the model itself could
be made trustworthy enough to skip the checking. It doesn't claim to
solve alignment — nothing I could build alone would. What it does is
narrower and, I think, more honest: it keeps a persistent, hash-chained
record of what an agent decided and why, refuses to let certain claims
get made without an explicit, checkable basis instead of a silent
default, and surfaces drift and contradiction before they compound
instead of after. It doesn't stop the first bad token. It makes the step
built on top of it attributable, and hard to erase after the fact. That's
a smaller promise than "safe AI" — but it's a real one, and it's one I
could actually ship rather than merely argue for.

I'm not claiming to have arrived anywhere final. Understanding this space
is a genuinely humbling process, and I expect to keep being wrong in new
ways as I keep going. What I want to build toward — with this project and
with what this grant would let me continue — is a starting point other
people don't have to bleed for the way I did: tools that give someone a
clearer view sooner, and a way to begin verifying that view for
themselves, instead of a promise to trust. A beginning, not an ending.
That's the whole ask.
