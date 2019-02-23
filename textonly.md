
Hi, I'm Eric. I'm here to talk about what seems like an absurd idea:
that if-then-else had to be invented.

---


If-then-else is how we talk about conditions in programming languages:
if something is true, then do a thing, else do a different thing.

That's just English, right? Except that it isn't.
I can't use "else" as a conjunction in normal speech,
only in computer programs.

Where did this `else` come from? It's a mystery.
It's too microscopic a detail to have made it
into books on the history of programming languages.

---


It doesn't seem to have come from surveys or legal proceedings or algorithms
as they were written before there were computers. You find "if yes" and "if no"
and "if however", but not "else".

* https://books.google.com/books?id=AH9Fs8huUGsC&pg=PA46#v=onepage&q&f=false
* https://archive.org/details/actsstateohio39statgoog/page/n189
* https://archive.org/details/in.ernet.dli.2015.463129/page/n85

---


The first computer to be able to perform different instructions
depending on the result of a previous calculation seems to have been the Eniac.
In 1946, Haskell Curry and Willa Wyatt wrote this report describing a program
to invert a function. They used the name "discrimination" for the
facility of making a decision based on which of two numbers was larger.

* https://apps.dtic.mil/dtic/tr/fulltext/u2/640621.pdf

---


The Eniac did not have an instruction called "discriminate."
It was programmed by wires and dials on plugboards, and the
control panel for the instruction that made a calculation for
a decision was connected by physical wires to the instructions
that could follow it.

Soon computers began to have enough memory that programs could be
stored in memory instead of wired together. Instead of a physical
sequence of instructions, there was a numerical sequence.
A few special instructions could cause the computer to jump
to a different point in the sequence.

* http://www.columbia.edu/cu/computinghistory/eniac.html

---


Here, for example, is the conditional jump instruction from one of
the first commercially produced computers. It checked whether the
last number calculated was negative.  If so, it diverted the flow of
control to some specified location in memory; otherwise, it let control
continue to the next instruction.

It was meant for a specific usage pattern: if you wanted to do a task,
say, 10 times, your program counted how many times it had done it so far
and then subtracted 10. If the result was negative, the task wasn't
done, so it jumped back to do another round.

* http://s3data.computerhistory.org/brochures/eckertmauchly.binac.1949.102646200.pdf

---


The idea was carried forward into the first higher-level
programming languages, like Halcombe Laning and Neal Zierler's
language for Whirlwind. Their conditional jump worked the same way,
except that the numbered steps of the program were algebraic
expressions, not single machine instructions.

* https://archive.computerhistory.org/resources/text/Fortran/102653982.05.01.acc.pdf

---


The first popular programming language, Fortran, generalized the idea
by specifying jumps to three locations at once, depending on whether
a calculation was negative, zero, or positive, and gave it the name "if."

The three-way "if" was more powerful than just checking for a negative,
but was probably more confusing, because every decision meant
a discontinuity in the control flow instead of programmers only having
to think about the normal case that continued on and the unusual case
that jumped.

* https://www.fortran.com/FortranForTheIBM704.pdf

---


Flow-Matic, Grace Murray Hopper's predecessor to COBOL, made the three-way if
a little easier to think about by talking about comparing two numbers instead
of about the signs of numbers. It introduced the name "otherwise" for
the case where the comparison wasn't what you were looking for.

* https://archive.org/details/bitsavers_univacflowProgrammingSystem1958_9367413/page/n39

---


All these programming languages were associated with one particular computer
from one particular manufacturer.  In 1958, two American and German computing
organizations began a joint project to develop a standard machine-independent
language, one that would natural for people to talk about rather than natural
to implement on some particular machine. Each group brought a draft proposal
to the joint conference.

* https://dl.acm.org/citation.cfm?id=800025

---


The German authors made two big conceptual leaps in their formulation of
the "if" statement.

The first was to let the conditional be controlled by any boolean expression
rather than giving special priority to the less-than/equal/greater-than form.

---


The second big leap was that instead of causing an abrupt jump in
the flow of control, their "if" statement only caused the flow to be
temporarily diverted. At the end of the condition, whether the condition
had been true or false, the program would resume at the "always" statement
at the end of the block. The only difference would be whether the
subsidiary statements had been performed.

The example on screen shows two "ifs" in a single block, and you might
think that the second one was intended to work as an "else if" does now. But
they expected all the conditions to be evaluated, even if one had already
been found to be true. So if the statements controlled by the first
changed a value that the second comparison depended upon, both blocks
of statements might execute.

* http://www.softwarepreservation.org/projects/ALGOL/report/BauerBRS-Proposal_for_a_Universal_Language-1958.pdf

---


Where the German proposal did have something like "else" was in a
second, entirely different, conditional form called "case."
Unlike "case" as we know it now, their "case" was another way
of writing boolean conditions, with the conditions set apart
in a separate block from the statements they controlled.
It sounds like they thought this form would be easier for
more complicated comparisons.

And here is the first appearance of the world "else," for the
case where none of the other cases apply.

* http://www.softwarepreservation.org/projects/ALGOL/report/BauerBRS-Proposal_for_a_Universal_Language-1958.pdf

---


Why did they call it "else?" They don't say.

What they do say is that this document was originally written in German
and hastily translated into English.
I think a carefully-chosen German word
was probably translated as an archaic English word and then never revisited.
Unfortunately we do not have the original German text to consult.

* http://www.softwarepreservation.org/projects/ALGOL/report/BauerBRS-Proposal_for_a_Universal_Language-1958.pdf

---


The American proposal also had the idea of controlling statements
by boolean expressions. It didn't even have an "if" keyword.
Instead, if an expression was followed by an arrow, the expression controlled
the statements that followed the arrow.

The notation doesn't make it obvious, but unlike the German block of ifs,
in the American form, if one expression in a block evaluated to true,
it did short-circuit and skip the following expressions, like "else if"
does now.

* http://www.softwarepreservation.org/projects/ALGOL/report/ACM_ALGOL_Proposal_1958.pdf

---


The two organizations held a joint meeting and merged their proposals
into a single document that they called the International Algebraic Language.
Before long the language would be renamed to Algol.

The "if" statement in the combined document looks a lot like the
German proposal, but eliminates the "always" statement to end the block.
Instead, each "if" stands alone, and if you want multiple statements
to be controlled by the same expression, you can use "begin" and "end"
to group them together.

There is nothing like "else" in this formulation of "if."

* http://www.softwarepreservation.org/projects/ALGOL/report/Algol58_preliminary_report_CACM.pdf

---


However, Algol 58 also had a second conditional form, called "if either."
In this form, you could say "or if" to do the same thing as we now do
with "else if." But there is nothing equivalent to "else" by itself,
without another "if."

* http://www.softwarepreservation.org/projects/ALGOL/report/Algol58_preliminary_report_CACM.pdf

---


The story gets muddy the next year, when several papers about Algol
were presented at a conference. One of them was the paper where John Backus,
who had previously led the Fortran project, introduced the idea of formal
grammars for programming languages.

Algol as he describes it doesn't have the "if either" conditional form.
Instead, it has a keyword called "converge," which makes the top-level
"ifs" inside its block behave like "else ifs." It is not clear whether
this was meant as an idea for a better "if either," or whether it was an earlier
idea that had already been rejected in favor of "if either."

* http://www.softwarepreservation.org/projects/ALGOL/paper/Backus-ICIP-1959.pdf

---


Either way, "if either" would soon be replaced. In 1957 John McCarthy
at MIT had written a proposal for the project that became LISP,
another extremely old programming language that still survives today.
His proposal introduced the idea of the conditional expression,
as opposed to the conditional statement.

The important distinction is that an expression must always have a value,
while a statement can simply not be performed if the condition that controls
it is not true.

So his "if function" always ends with a clause called "otherwise"
that gives the value of the expression when none of the other
conditions have evaluated to true.

* http://www.softwarepreservation.org/projects/LISP/MIT/McCarthy-CC-56.pdf

---


McCarthy's conditional expressions inspired Klaus Samelson to clean up
and unify Algol's two separate conditional models at the end
of 1959. He eliminated the entire "if either" form, leaving
only the plain "if," but added a clause called "else" that would
be performed when the expression controlling the corresponding "if"
had been false.

You could chain conditions together with "else if," just like
the previous "if either" had allowed with "or if," but you could
also use "else" by itself for a final set of statements that
would run if none of the conditions had been true.

* https://dl.acm.org/citation.cfm?id=1060889

---


"If-then-else" was the single conditional form that appeared in the Algol 60
report the next year, and is the form that almost all subsequent
programming languages have followed.

Although it seems clear to us now, it was hard for people in 1960 to think about,
and the report spends a page and a half explaining how it works,
including this arrow diagram.

* https://fi.ort.edu.uy/innovaportal/file/20124/1/14-naure_algol60.pdf

---


As I mentioned, the use of "else" as a conjuction sounds strange.
Christopher Strachey's CPL programming language is the grandparent
of C and therefore the ancestor of most current programming languages,
and he refused to use "else," calling it "ignorantly incorrect English."
He thought we should write "test … then … or" instead, which also
doesn't sound very natural, and didn't catch on.

* http://www.ancientgeek.org.uk/CPL/CPL_Elementary_Programming_Manual.pdf

---


The MAD programming language also went its own way. It was known
for its extremely long keywords, and in addition to using
"whenever" instead of "if," it used "otherwise" instead of "else"
and "or whenever" instead of "else if."

It is worth nothing the indentation in the MAD manual's example.
It took years before most other programming languages adopted
this style of indenting conditions, even though it now
seems unimaginable to do it any other way.

* http://www.bitsavers.org/pdf/univOfMichigan/mad/L2-UOI-MAD1-2-RX_MADum_62.pdf

---


But even while CPL and MAD shunned the word "else," they kept
the form and only changed the vocabulary. Language designers still search
for the perfect way to write a `for` loop, but the quest for
the perfect conditional form seems to have ended in 1959.
Thank you Klaus Samelson, for giving us a tool to think with
and a word to puzzle over.

* https://www.in.tum.de/en/the-department/history/
