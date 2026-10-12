# Style-0: Exploring Playing Styles with Machine Learning

*An experimental neural network developed for GoKifu.*

## The idea

Go players often associate professional players with distinctive styles.

Takemiya Masaki is famous for his influence-oriented approach, Kobayashi Koichi for his territorial efficiency, Lee Sedol for his creative and fighting-oriented play, and Shin Jin-seo for his modern, highly precise game.

But can a neural network actually recognize differences between how these players approach the game?

That's the question behind **Style-0**.

Rather than evaluating whether moves are good or bad, Style-0 explores whether patterns in board positions and move sequences can provide clues about a player's approach to Go.

The goal is to offer players a different perspective on their games: **which of these professional players does their play most closely resemble?**

## From professional games to a neural network

Style-0 was developed and trained using a dataset of over **5,000 professional Go games**.

The model focuses on four reference players:

- **Kobayashi Koichi**
- **Takemiya Masaki**
- **Lee Sedol**
- **Shin Jin-seo**

These players were selected to provide a diverse set of recognizable playing approaches, although their styles cannot be reduced to simple categories.

The fundamental challenge is that playing style isn't directly measurable. There is no objective label telling us whether a move is "creative", "territorial", or "aggressive".

Instead, Style-0 learns to distinguish between games played by different professionals and uses these learned representations to explore stylistic similarities.

## How it works

Style-0 combines two complementary ways of looking at a Go game.

**1. Understanding board patterns**

A Convolutional Neural Network (CNN) processes spatial representations of the board at different stages of the game.

This allows the model to learn patterns related to stone placement, formations, and the spatial organization of a position.

**2. Understanding move sequences**

A Transformer processes the chronological sequence of moves.

Unlike a static board representation, this preserves information about the order in which decisions were made.

It allows the model to learn relationships between moves occurring at different moments of a game.

**Combining both perspectives**

The two representations are brought together through an attention-based mechanism.

The resulting representation combines spatial information with the sequence of decisions that produced it.

Rather than relying exclusively on the final board position or individual moves, Style-0 attempts to capture patterns across the development of a game.

### Learning meaningful distinctions

During training, Style-0 also uses **Supervised Contrastive Learning (SupCon)**.

The general idea is to encourage the network to learn representations where examples from the same player are closer together, while examples from different players become more distinguishable.

This learning objective complements the classification task. It helps shape the representations learned during training rather than acting as a separate prediction engine.

The resulting model produces a distribution of scores across the four reference players.

**Style-0 is a custom-trained neural network, independent of KataGo and the GoKifu Coach. It does not use an LLM.**

## What players see in GoKifu

Style-0 is integrated directly into GoKifu's post-game reports.

After analyzing a game, players can explore their stylistic similarities with the four reference professionals.

The report displays the closest matching professional, alongside the relative scores for the other reference players.

Both Black and White are analyzed independently.

It's intended as an additional perspective on a game, separate from KataGo's move evaluations and the Coach's strategic explanations.

## Understanding the limitations

Playing style is difficult to define, even among human Go players.

And Style-0 has important limitations.

**Recognizing a professional player's games is not the same as objectively measuring playing style.**

The model may learn patterns associated with opening preferences, historical periods, or other characteristics of its training data, rather than purely abstract strategic tendencies.

Its predictions are also limited to four reference professionals. A high score does not mean a player genuinely plays like that professional in every respect, and the displayed percentages should not be interpreted as scientifically calibrated measures of style similarity.

Style-0 is best understood as an experimental comparison within a limited reference set, not a definitive classification of how someone plays Go.

## An ongoing experiment

Style-0 has gone through several iterations, involving different architectures, training strategies, and evaluation approaches.

The project has also highlighted how important careful validation is when training models on professional game collections. Apparent improvements are only meaningful when the evaluation methodology is reliable.

There's still plenty to explore, from improving the model's generalization to understanding which features it actually learns to associate with individual players.

For me, Style-0 is an opportunity to experiment with machine learning on a subject I care about.

It's also an example of another aspect of GoKifu's development: beyond integrating established tools such as KataGo, I've been interested in designing, training, and evaluating my own models to explore different ideas around Go.

Style-0 isn't a finished answer to what makes a playing style.

It's an experiment that I'm continuing to learn from.