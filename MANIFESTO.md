# The GoKifu Manifesto
## Built for Go players. Not for the AI hype.

### Why I started GoKifu

I started working on GoKifu over two years ago.

At the time, I was looking for a mobile app that would let me comfortably record my games, manage my SGF files, and analyze my mistakes using a strong Go engine.

There were surprisingly few convincing options combining these things into a good experience. AI Sensei was already an excellent reference for game analysis, but I wanted to build something of my own, with a different approach to the overall experience.

I'm a dan-level Go player and a software developer. GoKifu started as a personal project combining those two interests.

It wasn't originally about building an AI coach.

It was about building the Go application I wanted to use.

Over time, the project grew. I added game analysis, professional game databases, and playing style analysis through Style-0, a custom-trained neural network.

Eventually, I started working on a much harder problem: how to make all this analysis more useful to the player.

That's where the GoKifu Coach came from.

### 1. KataGo is incredibly strong. Understanding its analysis is another challenge.

KataGo can identify better moves, evaluate positions, estimate territory, and explore variations at a level far beyond most human players.

But a score difference doesn't automatically tell you what you should learn from a mistake.

Losing five points because you misread a sequence to save a weak group isn't the same lesson as losing five points by playing in the wrong direction.

The numbers might be similar. The underlying decisions are different.

I want GoKifu to help players recognize those differences.

Not just where the game went wrong, but what kind of mistake they made.

### 2. Why the Coach doesn't use an LLM

Let's be clear about the architecture.

**The GoKifu Coach does not use a large language model to generate its explanations.**

Current LLMs are not reliable Go analysts, they often struggle with actual board positions, tactical sequences, and strategic reasoning.

Giving a language model KataGo's evaluations doesn't automatically make its explanations correct.

So I chose a different approach.

GoKifu takes KataGo's analysis data, including score estimates, move evaluations, ownership information, and variations, and processes it through a custom rule-based event detection system.

That system attempts to identify meaningful situations: missed priorities, weak groups, changes in territorial control, important attacks, and defensive opportunities.

The Coach then produces structured explanations using predefined rules and connects them to the relevant areas and moves on the board.

**No LLM is involved in writing the commentary.**

This doesn't guarantee that every explanation is correct. But it means the explanation comes from explicit analytical conditions rather than freely generated prose.

And those conditions can be inspected, tested, and improved.

### 3. The explanation should be connected to the board.

Consider a player who reinforces an already secure area while a weak group elsewhere needs attention.

KataGo might show that the move loses several points and recommend playing on the other side of the board.

But for the player, the important lesson is the missed priority.

That's the kind of situation I want GoKifu to recognize.

Another example: a player has an opportunity to attack a weak group but plays elsewhere, allowing the opponent to stabilize.

Rather than simply marking the move as a mistake, the Coach should help identify the missed opportunity, the group involved, and the relevant alternative.

The board itself is essential here.

GoKifu uses visual markers and explorable variations to connect its explanations to the actual position.

A good explanation should be something you can investigate on the board, not just something you read and accept.

### 4. Not every move needs an explanation.

I don't think a useful Go review should bury players under hundreds of comments.

Most games have a handful of important turning points, missed opportunities, or recurring mistakes that deserve attention.

I'd rather help someone understand three meaningful decisions than give them fifty paragraphs of commentary.

The goal is to select useful moments, not generate as much content as possible.

### 5. A rule-based Coach can still be wrong.

This is important.

KataGo is a neural network. GoKifu's interpretation of its output is built from heuristics and rules that I've developed and continue to refine.

Detecting a score loss is relatively straightforward.

Identifying the strategic reason behind it is much harder.

Sometimes the system will misclassify an event. Sometimes an explanation will miss an important detail. Sometimes a perfectly reasonable move will be described in a misleading way.

These are real limitations, and I don't want to hide them.

But with explicit rules, I can investigate why an event was detected, adjust the underlying logic, and test whether the change actually improves the results.

That's the approach I've chosen.

It doesn't replace human teaching, and I don't expect it to.

### 6. Beyond KataGo: Experimenting with Style-0

GoKifu isn't just about integrating existing Go engines. I've also been exploring my own approaches to machine learning.

One of these experiments is **Style-0**, a neural network I designed and trained on over 5,000 professional games to explore whether playing styles can be recognized from board positions and move sequences.

The model combines spatial and sequential representations with supervised contrastive learning, attempting to identify stylistic similarities with four professional players: Kobayashi Koichi, Takemiya Masaki, Lee Sedol, and Shin Jin-seo.

Style-0 is now integrated into GoKifu's game reports, offering players a different perspective on their games: not just how well they played, but whose playing style their decisions most closely resemble.

Of course, playing style is difficult to define objectively, and the model remains experimental. Its predictions shouldn't be treated as definitive judgments.

But Style-0 also represents another side of what I've been building over these two years: **not only using existing AI tools, but designing, training, evaluating, and integrating my own models to explore new ideas around Go.**

For me, that's a big part of what makes working on GoKifu interesting.

### 7. Two years of development, and still learning.

GoKifu has grown considerably since I started it.

And so has the ecosystem of Go applications.

There are now many new tools appearing, which I think can be a good thing for the Go community.

But I believe tools deserve to be judged by what they actually do, how well they work, and whether they help players improve.

Not by how many AI features they advertise.

GoKifu is an independent project, developed by someone who genuinely enjoys both Go and software engineering.

I'm still experimenting, still finding flaws in the Coach's interpretations, and still improving the application.

I'd especially welcome feedback from experienced players who are willing to challenge its explanations.

**If the Coach identifies the wrong strategic problem, I want to know.**

---

### What I'm trying to build

I started GoKifu because I wanted a better application to record and study my own games. Two years later, that's still what motivates me.

The Coach, Style-0, and the other features are all part of that ongoing process of experimenting, learning, and trying to make something genuinely useful.

There's still a lot I want to explore and improve, and I'm always interested in hearing what other Go players think, especially when something doesn't work as intended.

At the end of the day, I'm just a Go player who enjoys building software, trying to create the kind of application I'd like to use myself.