# The GoKifu Coach: Making Sense of KataGo Analysis

*A rule-based approach to interpreting Go games, without LLM-generated commentary.*

## The idea

KataGo is an incredibly powerful Go engine.

It can evaluate positions, explore variations, estimate territorial ownership, and identify moves that are stronger than those played by most humans.

But interpreting that information isn't always straightforward.

Losing five points because you misread a sequence to save a weak group isn't the same lesson as losing five points by playing in the wrong direction.

Did you miss an opportunity to attack? Fail to defend an important group? Overlook a critical move? Or repeatedly ignore the same strategic priority?

**The numbers might be similar. The underlying mistakes, and what you can learn from them, are different.**

That's the problem I've been exploring with the **GoKifu Coach**.

The goal is to identify meaningful patterns in KataGo's analysis and turn them into observations that players can investigate and learn from.

## How it works

The Coach is built around three main components.

### 1. KataGo: The analysis engine

Everything begins with KataGo.

It provides the underlying position evaluations, candidate moves, variations, estimated territorial ownership, and other information about the state of the game.

KataGo is responsible for the actual Go analysis.

The Coach doesn't attempt to replace that engine or independently determine which moves are best.

Instead, it builds on the information KataGo provides.

### 2. The GoKifu Interpretation Engine

KataGo's raw outputs are useful, but they aren't directly equivalent to human Go concepts.

For example, a drop in KataGo's ownership estimates may suggest that a group has become vulnerable. But that doesn't necessarily mean defending it was the right move. KataGo might actually favor attacking an opponent's group elsewhere, while the change in stability is only a secondary consequence of the position.

To bridge this gap, I've been developing the **GoKifu Interpretation Engine (GIE)**.

It's a collection of custom metrics and analysis methods that examine different aspects of a position and how they evolve throughout a game.

Among other things, it explores:

- **Group stability:** How the estimated security of groups changes during a game.
- **Move alternatives:** Whether a position offers several reasonable choices or very few.
- **Territorial changes:** How estimated control of different areas evolves.
- **Group transitions:** How groups become stronger, weaker, connected, separated, or captured.
- **Decisions over time:** Whether similar opportunities or problems appear repeatedly throughout a game.

These measurements provide the foundation for the Coach's observations.

They are interpretations of engine data, not objective proofs of strategic intent.

### 3. The Coach: From observations to explanations

The Coach processes those measurements using a custom rule-based system.

Rather than trying to explain every move, it looks for recognizable events.

Some examples include:

**Missed priorities**

A player chooses one area of the board while KataGo consistently favors a different region containing stronger alternatives.

**Weak groups and missed defenses**

A group's estimated stability deteriorates, potentially revealing an important defensive problem.

**Attacking opportunities**

A group becomes more secure after the player chooses to play elsewhere, potentially indicating a missed opportunity to maintain pressure.

**Critical decisions**

A position offers very few competitive alternatives, making the choice of move particularly important.

**Recurring patterns**

The same move or group repeatedly becomes relevant across several decisions, suggesting a pattern worth reviewing rather than treating each occurrence independently.

These events are only the starting point.

Detecting that a group became weaker does not necessarily establish *why* it happened.

For that reason, the Coach also examines relationships between observations, played moves, and alternatives suggested by KataGo.

When those relationships provide sufficient evidence, it can formulate a more specific interpretation, such as a missed defense or an unfavorable exchange.

When they don't, a more descriptive observation may be more appropriate.

This distinction between **observing a change and explaining its cause** is one of the central challenges of the project.

## Why there's no LLM

**The GoKifu Coach does not use a large language model to generate its commentary.**

This is a deliberate design decision.

Current LLMs are not reliable Go analysts. They struggle with reading board positions, following tactical sequences, and understanding strategic decisions.

Giving a language model KataGo's evaluations doesn't suddenly give it the ability to understand Go. It still lacks the reasoning needed to reliably explain why a move is better than another.

I wanted to explore a different approach.

The Coach uses explicit rules to identify events, examine relationships, and select relevant observations.

Those observations are then expressed through predefined, localized language templates.

There is no generative language model involved in writing the explanations.

This doesn't guarantee that the resulting commentary is correct.

But it means the explanations are produced by identifiable analytical conditions that can be examined, tested, and refined.

The goal is not to generate commentary that sounds convincing. It's to improve the connection between what the analysis actually shows and what the Coach tells the player.

## Keeping explanations focused

One challenge I encountered during development was information overload.

A single move can trigger several observations. It might weaken one group, strengthen another, and miss an important alternative elsewhere.

Listing every detected event doesn't necessarily produce a useful explanation.

It can actually make the underlying decision harder to understand.

To address this, the Coach includes a selection and interpretation process that tries to identify the most relevant information, avoid redundant commentary, and keep explanations relatively short.

Other observations can still contribute to the broader game report without appearing in the immediate commentary.

I don't think the value of a Go review should be measured by how many sentences it produces.

Sometimes one useful observation is enough.

## Connecting explanations to the board

Text alone isn't always the best way to explain Go.

When the Coach refers to a particular group, it can highlight the corresponding stones directly on the board.

Players can examine the alternative moves and variations provided by KataGo.

The idea is to keep the explanation connected to the position rather than asking players to accept a written conclusion at face value.

This is especially important because an explanation may be incomplete.

Being able to inspect the actual variation gives players the opportunity to question what the Coach says and reach their own conclusions.

The Coach is intended to complement the analysis, not replace it.

## Testing and improving the system

One of the most difficult aspects of this project has been evaluating the quality of the explanations.

An event can satisfy its detection conditions and still produce a misleading interpretation.

For example, a group may appear to become less stable after a move, but that doesn't prove the group was the main strategic concern in the position.

The real reason KataGo preferred another move might involve attacking an opponent, preserving sente, or a tactical continuation that the heuristic system hasn't captured.

When I first introduced the Coach on [r/baduk](https://www.reddit.com/r/baduk/comments/1vfmqqz/would_an_ai_coach_that_translates_katago_into/), several experienced players pointed out exactly this kind of problem.

That feedback highlighted an important distinction: **detecting the consequences of a move isn't necessarily the same as identifying the reason behind KataGo's recommendation.**

Since then, I've continued refining the detection and interpretation process, using real-game examples, regression tests, and comparisons between different approaches.

Some ideas work well in theory but turn out to be too noisy or misleading when tested against actual games.

Others require additional evidence before they can produce useful commentary.

Part of developing the Coach is learning which observations are worth keeping, which need better interpretation, and which should simply be discarded.

## Current limitations

The Coach is still experimental, and its limitations are important.

It can misidentify the main strategic issue, overlook tactical details, or overemphasize consequences that aren't particularly relevant to the player's decision.

Some positions are simply too complex to summarize reliably using the patterns currently implemented.

There is also a difference between explaining KataGo's preferred move and providing the most useful lesson for a particular player's level.

An observation that helps a beginner may be obvious to an experienced player. Conversely, a simplified explanation can become misleading if it omits an essential tactical detail.

I don't consider these problems solved.

The current approach is to work with a limited set of detectable patterns, improve their reliability through testing, and avoid assuming that every position has a simple explanation.

**A rule-based system can still be wrong. What matters is being able to investigate why.**

## An ongoing experiment

The Coach is one part of GoKifu, alongside game recording, SGF management, KataGo analysis, and Style-0.

Unlike Style-0, which is a separately trained neural network, the Coach relies on deterministic analysis and interpretation rules built around KataGo's outputs.

They're different approaches to different problems.

I don't expect the Coach to replace human teachers, and I don't think a handful of metrics can capture everything that makes Go strategically interesting.

But I believe there's a lot worth exploring between raw engine evaluations and useful explanations.

For now, that's what I'm working on: experimenting with different ways to interpret KataGo's analysis, testing them on real games, and gradually improving the results.

And if an explanation gets something wrong, I'm interested in understanding why.