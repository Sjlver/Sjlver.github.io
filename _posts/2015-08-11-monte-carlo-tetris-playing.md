---
layout:     post
title:      "Monte Carlo Tetris Playing"
date:       2015-08-11 22:30:00
categories: technology
---

Programming is wonderful! Literally *full of wonders*. As you write code, it
becomes complex, unpredictable, and surprising and you, the author, are never
quite sure what it will do. Last weekend, I wrote parts of an AI for a
Tetris-like game. It is based on an algorithm called Monte Carlo Tree Search.
The approach is deceptively simple, but fascinating...

See for yourself in this screencast:

<script type="text/javascript" src="https://asciinema.org/a/24875.js" id="asciicast-24875" async>
</script>

This program was my team's entry to the [International Contest in Functional
Programming][icfp], a weekend-long programming competition. The contest
challenges participants to save the world by playing a Tetris-like game on a
hexagonal grid. Participants write a program that receives a specification of
the grid, the blocks and their order, and a time limit within which it needs to
produce a sequence of moves. Programs receive points for every block played and
for lines cleared. There were additional challenges in the competition, but this
blog post focuses on our Tetris AI.

How do computers play Tetris? Our program does it very differently than a human
being would. Human players use various heuristics, like keeping the stacks low or
avoiding holes. In contrast, the AI is based almost entirely on simulation and
on a clever strategy called [*Monte Carlo Tree Search*][mcts]. Here is how it
works:

For every move, the AI evaluates hundreds of alternatives, and chooses the most
interesting one based on *random playouts*. A random playout simply means: "make
random moves until the game ends, and report the final score." Moves with a high
average playout score are probably better than moves with a low average playout
score.

In our program, this looks as follows (actual, just slightly simplified code.
Would you guess this plays Tetris?):

{% highlight scala %}
def addPlayout() {
  val playoutBoard = board.clone()
  while (playoutBoard.isActive) {
    playRandomMove(playoutBoard)
  }

  numPlayouts += 1
  sumScores += playoutBoard.score
}
{% endhighlight %}

One problem is that there are billions of move combinations, many more than the
AI could ever evaluate. This is where Monte Carlo Tree Search has a really
clever solution: a playout is always added to the *most interesting* move, where
interestingness takes both exploration and exploitation into account.

Exploration means that the AI tries to explore moves that it knows little about.
It wants to explore the move with the fewest number of playouts. Exploitation
means that the AI should not waste time on bad moves. It want to explore the
move with the highest average score.

Here's an example for a particular game situation:

    . . . . . . . . . .
     o . . ● ● ● . . . .     move |  avg score   playouts
    o o o . . . . . . .      -----|----------------------
     o o o . . o o o . .       E  |        666        233
    o o . . . o o o o .        W  |        651        205
     . o . . o o o . . o      SE  |        641        189
    . . o o o o o . o o       SW  |        645        195
     . . o . o . o o o o      CW  |        662        225
    . o o o o o o o o o      CCW  |        671        247
     . . o . o o o o o .
  
Here, the AI has most deeply explored moves starting with rotating
counter-clockwise. It has spent 247 of its playouts on that option (mostly on
the combination "rotate counter-clockwise, then move south-west, then ...") If
it were to perform more explorations, it would explore "go south-east, then
rotate clockwise, then" because that move is relatively unexplored.

After all these evaluations, the AI chooses to rotate counter-clockwise. It does
not necessarily choose the options with the highest score (although in this case
CCW does have the highest score). Instead, it chooses the option with most
playouts, because that move has consistently been interesting.


Bugs'n'Pieces
-------------

Completely random playouts are a rather stupid way of evaluating how promising a
move is. In the situation above, most sequences of random moves immediately lose
the game. I believe that adding a few heuristics to the playout would be the
single most effective way of improving our AI.

I learned a lot about hexagonal grids during this weekend. The [Hexagonal Grids
page from Red Blob Games][hexgrids] has been a treasure trove of information
about rotations, cube coordinates, and much more.

One last story I want to tell is about a really interesting bug that we've
produced during the contest. We found it while watching the AI play, and
thinking "hey, this is curious...?" The game rules specify that a block needs to
be centered at the top of the grid when it enters play. To center it, our code
first computes the width of the block. It turns out that on a hexagonal grid,
this is not so easy, because *the width depends on the vertical position of the
block.*

This was very counter-intuitive to me, but here is an example:

                     columns used         width
    . . . ● . . .               4
     . ● ● . . .             2, 3         2 to 4 = 3
    . . . ● . . .               4
     . . . . ● .                5
    . . . ● ● . .            4, 5         4 to 5 = 2
     . . . . ● .                5

This issue caused us to spawn the block in the wrong position. Because of this,
our solution received zero points whenever the game contained blocks of that
particular shape... until we found and fixed the bug.

[Our code is now open-source.][int4t_code] If you like it or have comments, let
me know!

[icfp]: http://icfpcontest.org/
[mcts]: https://en.wikipedia.org/wiki/Monte_Carlo_tree_search
[hexgrids]: http://www.redblobgames.com/grids/hexagons/
[int4t_code]: https://github.com/Sjlver/icfp-2015
