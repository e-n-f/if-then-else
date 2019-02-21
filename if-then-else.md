Hi, I'm Eric Fischer, and I'm here to talk about what seems like
a fairly absurd idea: the idea that if-then-else had to be invented.

* …

If-then-else is how we talk about conditions in programming languages:
*if* something is true, *then* do a thing, *else* do a different thing.

That's just English, right? Except that it isn't. I am a native speaker
of English, and I can't use "else" as a conjunction in normal speech,
only in computer programs.

So where did this `else` come from? No one seems to have written about it.
It's too microscopic a detail to have made it
into any books on the history of programming languages.

* https://books.google.com/books?id=AH9Fs8huUGsC&pg=PA46#v=onepage&q&f=false
* https://archive.org/details/actsstateohio39statgoog/page/n189

To understand why programmers talk about conditions the way they do,
I thought it might help to look at how conditional processes were
described before there were computers.

It is actually hard to find good examples of these.
About as close as you can come are surveys and legal procedures 
that require you to answer certain questions only if you answered
yes to a different question. But for the alternative cases,
they say "if yes" or "if no," not "else."

* https://archive.org/details/in.ernet.dli.2015.463129/page/n85

And there are mathematical algorithms, like taking a cube root, that
involve some guesswork, and require repeating a step if you guessed wrong.
But algorithms were mostly described in terms of repetition,
not in terms of making decisions, and I haven't found any examples
of "else" being used when they do talk about decisions.

* https://apps.dtic.mil/dtic/tr/fulltext/u2/640621.pdf

The first computer to be able to automatically perform a different set of instructions
based on the result of a previous calculation seems to have been the Eniac.
In 1946, Haskell Curry and Willa Wyatt wrote a report describing how to
use the Eniac to invert a function and interpolate values.
They used the name "discrimination" for the facility of making a decision
based on which of two numbers was larger.

* http://www.columbia.edu/cu/computinghistory/eniac.html

The Eniac was programmed by connecting wires on plugboards, so
they did not have an instruction called `discriminate.` They had
physical wires connecting the control panel for one instruction
to the control panels of the instructions that could follow it.

Very soon, though, computer programs began to be stored in memory
rather than wired together. In memory, instructions are normally
performed in numeric sequence, one after the other. A few special
instructions can change this sequence by jumping forward or back
to a different point in the sequence, either unconditionally or
only in some particular circumstance.

* http://s3data.computerhistory.org/brochures/eckertmauchly.binac.1949.102646200.pdf

Here, for example, is the conditional jump instruction from the BINAC, one of
the first commercially produced computers. It checked whether the machine's
accumulator contained a negative number. If it did, it diverted the flow of
control to some specified instruction; otherwise, it let control continue
normally to the next instruction.

This instruction was designed to support a specific usage pattern:
if you wanted to do a thing several times, at the end of each iteration
you subtracted the total number of iterations you wanted to make from
the number of the current iteration. If the
result was negative, that meant you weren't done yet, so you jumped back to do
another round of calculation.

* https://archive.computerhistory.org/resources/text/Fortran/102653982.05.01.acc.pdf

This same idea was carried forward into the first higher-level
programming languages, like Halcombe Laning and Neal Zierler's
language at MIT for Whirlwind.  It followed exactly the same paradigm,
except that the numbered steps of the program were evaluations of
algebraic expressions, not single machine instructions.

* https://www.fortran.com/FortranForTheIBM704.pdf

The first widely used programming language was Fortran, from IBM,
and it generalized this paradigm a little bit. Instead of checking
whether the result of a calculation was negative, its "if" statement
checked whether an expression was negative, zero, or positive, and
jumped to one of three different locations in the program depending
on which it was.

This should theoretically have been more powerful than just checking
for a negative, but was probably actually just more confusing,
because it meant you *always* had to think about discontinuities in the flow of
control instead of being able to make a clean distinction between the
normal condition in which you continue on to the next step, and the
unusual condition in which case you have to do something different.

* https://archive.org/details/bitsavers_univacflowProgrammingSystem1958_9367413/page/n39

One way of making these three-way comparisons a little easier to think
about came from Flow-Matic, a programming language from Remington Rand
for business applications. It was Grace Murray Hopper's project before
COBOL, and many of its concepts were carried forward into COBOL.

In Flow-Matic, instead of looking at the sign of a number, you
said to compare two numbers, and then said where you wanted to jump
if the first number was less than, equal to, or greater than the
second. You still had to think about all of these as jumps in the
flow of control, but the jumps were based on comparisons, not on
arithmetic signs, so they were one step closer to talking about
conditions in a natural way.

That same year, two different national organizations began projects
to develop programming languages that were not tied to one particular
machine from one particular manufacturer. This machine independence
also meant they could try to think about what would be the most
natural way to talk about a process rather than what was the most
straightforward to implement on some particular machine.

* http://www.softwarepreservation.org/projects/ALGOL/report/BauerBRS-Proposal_for_a_Universal_Language-1958.pdf

The German authors of the "Proposal for a universal language for
the description of computing processes" made two big conceptual leaps
in how their "if" statement was formulated.

First, instead of giving special privilege to the three-way
less-than/equal/greater-than comparison form, their "if" statement
accepted arbitrary boolean expressions. You could calculate and
compare with as much complexity as you needed, including ands and ors,
as long as the final result ended up with a true or false value.

The second big leap was that instead of causing the flow of control
to jump around, their "if" statement caused only a temporary diversion,
just enough to let a series of statements subsidiary to
the condition to be executed. Afterward, whether the expression had
evaluated to true or to false, you would always end up at the
"always" statement at the end of the block, and the only difference
would be whether or not the subsidiary statements had been performed.

This looks almost like "if" as we now know it, including the idea
that there could be multiple ifs in a single block for different
conditions. But it is important to realize that they expected
all of the "ifs" to be evaluated, even if the first one had already
been determined to be true. So if the statements controlled by
the first if changed a variable that the second comparison depended upon,
both blocks of statements might execute.

* http://www.softwarepreservation.org/projects/ALGOL/report/BauerBRS-Proposal_for_a_Universal_Language-1958.pdf

Their proposal also included another entirely different conditional
form, called "case." It is unrelated to what "case" now means in
programming languages, and instead was another way to write boolean
expressions, with the expressions set apart in a separate section from the statements
they controlled.  It appears that the reason to have both forms was
that you could put ifs inside cases, for nested comparisons.

In addition to the boolean expressions they also included a case
called "else," which seems to be the first use of the word in
programming languages. It denoted the case where none of the other
cases were true: the remainder, as they referred to it.

Why did they call it "else?" They don't say.

* http://www.softwarepreservation.org/projects/ALGOL/report/BauerBRS-Proposal_for_a_Universal_Language-1958.pdf

The best explanation for the word choice may be this note.
We are looking at a document that was originally written in German
and was hastily translated into English by someone whose native language
was not English. A carefully-chosen German word
was probably translated as an archaic English word and then never revisited.
Unfortunately we do not have the original German text to consult.

* http://www.softwarepreservation.org/projects/ALGOL/report/ACM_ALGOL_Proposal_1958.pdf

The other proposal for a machine-neutral programming language
came from the Association for Computing Machinery in the United States.
It took the the idea of controlling statements by boolean expressions a step further:
there wasn't even an "if" keyword; if an expression was followed
by an arrow, then the expression controlled the statements that
followed the arrow.

This form also gets very close to if-then-else as we now know it.
In particular, if you had a series of expressions and the statements
that they controlled on the same line, and one expression had
evaluated to true, all the rest of the expressions on the line
would be short-circuited and skipped. This was just like "else if"
as we use it now, but there was nothing corresponding to "else"
without another if.

* http://www.softwarepreservation.org/projects/ALGOL/report/Algol58_preliminary_report_CACM.pdf

The US and German organizations held a joint meeting at a conference
in Switzerland and merged their proposals into a single document
that they called the International Algebraic Language, and would
be subsequently renamed to Algol.

The "if" statement in the combined document came out looking
mostly like the German proposal that had gone in, except that
they eliminated the "always" terminator. This was possible because
they also introduced "begin" and "end" keywords to group statements
into blocks, so if there were multiple statements to be controlled
by an "if," you could put them together into a block instead of
needing the "always" to indicate where the block of controlled
statements ended.

* http://www.softwarepreservation.org/projects/ALGOL/report/Algol58_preliminary_report_CACM.pdf

The Algol "if" construction didn't have anything like "else."
Instead, they had a second conditional form called "if either,"
that *did* have its own "end" statement at the end of a block of
ifs, and used "or if" for what we would now call "else if." Like
the American proposal that had gone in, the "if either" form still
didn't have the idea of an "else" that was not followed by another if.

* http://www.softwarepreservation.org/projects/ALGOL/paper/Backus-ICIP-1959.pdf

The next year, the story gets very muddy. There were several papers
presented about Algol at another conference in Paris in 1959, and
one of them is the famous paper where John Backus, who had previously
led the Fortran project, introduced the idea of formal grammars for
programming languages.

As described in his paper, Algol does not have the "if either"
conditional form. Instead, it has another keyword called "converge,"
which causes the top-level ifs within the block to behave like "else
ifs." Was this a proposal for a better "if either," or was it
an earlier draft of what had already become "if either," published
after it was already obsolete?  There is no documentation to say
which it was.

* http://www.softwarepreservation.org/projects/LISP/MIT/McCarthy-CC-56.pdf

In either case, "if either" would not last for much longer.
In 1957, John McCarthy at MIT had written a grant proposal
for a project that eventually became LISP, one of the other
extremely old programming languages that still survives today.
The language he proposed looks nothing like what LISP soon
became, but introduced the idea of the conditional expression,
as opposed to the conditional statement. The important
distinction here is that an expression must always have a value,
no matter what happens, as opposed to a statement which can
simply not happen if the condition that controls it is not true.
So McCarthy's "if function" always contains a clause called "otherwise."
"Otherwise" gives the final value of the expression when none of the
other conditions in the if function have evaluated to true.

* https://dl.acm.org/citation.cfm?id=1060889

This model of conditions inspired Klaus Samelson to clean up
and unify Algol's two separate conditional models at the end
of 1959. He eliminated the entire "if either" form, leaving
only the plain if, but added a clause called "else" that would
be performed when the expression controlling the corresponding "if"
had been false.
You could chain conditions together with "else if," just like
the previous "if either" had allowed with "or if," but you could
also use "else" by itself for a final set of statements that
would run if none of the conditions had been true.

* https://fi.ort.edu.uy/innovaportal/file/20124/1/14-naure_algol60.pdf

This was the single conditional form that appeared in the Algol 60
report the next year, and is the form that almost all subsequent
programming languages have followed. If-then-else was apparently
not easy for people in 1960 to think about, because the Algol
report spends a page and a half explaining how it works, including
this arrow diagram and the
explation that "else" by itself is equivalent to "else if true then."

* http://www.ancientgeek.org.uk/CPL/CPL_Elementary_Programming_Manual.pdf

As I said at the start, this use of "else" as a conjunction
sounds strange to English speakers, and it did not take
long before some objections to it were raised. One was from
Christopher Strachey, designing the CPL programming language.
CPL was the grandparent of C and therefore the ancestor of
most programming languages in use today. He called "else"
"ignorantly incorrect English" and "egregiously incorrect,"
and wanted to use "test … then … or" instead. But that doesn't
sound very natural either, and it didn't catch on.

* http://www.bitsavers.org/pdf/univOfMichigan/mad/L2-UOI-MAD1-2-RX_MADum_62.pdf

The MAD programming language from the University of Michigan 
also went its own way. MAD was known
for its extremely long keywords, and in addition to using
"whenever" instead of "if," it used "otherwise" instead of "else"
and "or whenever" instead of "else if."

It is worth nothing the indentation in the MAD manual's example
of how to use "or whenever" and "otherwise." It was years before
most other programming languages adopted this style of indenting
the statements controlled by conditions, even though it now
seems unimaginable to do it any other way.

* https://www.in.tum.de/en/the-department/history/

But even while CPL and MAD shunned the word "else," they kept
the form and only changed the vocabulary. Language designers still search
for the perfect way to write a `for` loop, but the quest for
the perfect conditional form seems to have ended in 1959.
Thank you Klaus Samelson, for giving us a tool to think with
and a word to puzzle over.
