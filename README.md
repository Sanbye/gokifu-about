# GoKifu

**Record your games. Explore KataGo analysis. Go beyond the best move.**

GoKifu is an Android application for Go (Baduk/Weiqi) players, combining game recording, SGF management, AI-powered analysis, and tools to better understand your games.

I'm a dan-level Go player and software developer, and I've been working on GoKifu for over two years.

The project started because I couldn't find a mobile application that brought together a comfortable game recorder, proper SGF management, and powerful AI analysis in an experience I genuinely enjoyed using.

Over time, GoKifu has grown to include a professional game database, interactive KataGo analysis, variation exploration, style detection (my custom AI **style-0**) and more recently, the **GoKifu Coach**.

## The GoKifu Coach

KataGo can tell you which moves are better and how many points you lost. But understanding *why* a decision was wrong is another challenge.

The GoKifu Coach is an attempt to bridge that gap.

Rather than using an LLM to generate commentary, it relies on a custom **rule-based event detection system** built around KataGo's analysis data.

It attempts to identify meaningful patterns such as missed priorities, weak groups, attacking opportunities, and territorial changes, connecting its explanations to visual markers and variations on the board.

**No LLM-generated commentary. No chatbot pretending to understand Go.**

This approach isn't infallible. Interpreting Go positions is difficult, and the Coach can still misidentify events or produce incomplete explanations. Improving that reliability is an ongoing part of the project.

## Style-0: Exploring Playing Styles with Machine Learning

Beyond game analysis, GoKifu also explores how machine learning can identify patterns in the way people play Go.

**Style-0** is a custom neural network trained on over 5,000 professional games to recognize stylistic similarities with four legendary players: **Kobayashi Koichi, Takemiya Masaki, Lee Sedol, and Shin Jin-seo**.

Its architecture combines board position representations and move sequences, using **Supervised Contrastive Learning (SupCon)** to learn meaningful distinctions between playing styles.

Integrated into GoKifu's game reports, Style-0 offers players a different perspective on their games: not just how well they played, but whose playing style their decisions most closely resemble.

Unlike the rule-based Coach, Style-0 is a separately trained neural network. It's an experimental approach to style recognition, not a definitive judgment of a player's identity or abilities.

## Why this repository exists

This repository is the public home for GoKifu's philosophy, technical explanations, and real examples of its analysis.

I created it to make the ideas and engineering behind GoKifu more transparent, particularly how the Coach interprets KataGo's output without relying on generative language models.

Here, I want to share:

- **Our manifesto:** The story behind GoKifu, its philosophy, and what I'm trying to build.
- **How the Coach works:** An accessible explanation of its architecture and event detection approach.
- **Real examples:** Actual Go positions, KataGo evaluations, and Coach explanations that can be examined and challenged.
- **Limitations and lessons learned:** Where the system struggles, what players have pointed out, and how it evolves.

This is not the application's source code repository. It's a place to document the reasoning behind the project and encourage constructive discussion.

## Built for Go players, with Go players

GoKifu is an independent project, and feedback from the Go community plays an important role in its development.

I first introduced the Coach concept on [r/baduk](https://www.reddit.com/r/baduk/comments/1vfmqqz/would_an_ai_coach_that_translates_katago_into/), where several players challenged its explanations and raised valuable questions about interpreting engine evaluations.

That feedback is exactly what I want to encourage here.

---

*GoKifu is a work in progress, built out of a love for Go and software engineering.*