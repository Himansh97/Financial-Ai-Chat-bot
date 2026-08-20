# Financial document chatbot

A prototype that answers plain-English questions about 10-K and 10-Q filings —
"has revenue grown year on year", "what are the stated risk factors" — by pulling
the figures out of the filings and explaining them.

Built during BCG's GenAI virtual experience on Forage. It is a simulation
exercise, not production work, and is here because the design choice in it is one
I have kept making since.

## The design choice

Extraction is **rule-based over parsed financial statements**, and the language
model only explains what extraction found. It is never asked to read a filing and
report a number.

That split matters more in finance than almost anywhere else. A model asked for
"revenue growth" will produce a confident, plausible, wrongly-rounded figure, and
nothing downstream can tell it apart from a right one. Deriving the figure
deterministically and letting the model do only the part it is good at — turning
a computed number into a sentence a person can read — means the arithmetic is
checkable and the prose is disposable.

The same idea, taken much further and with a signed audit trail behind it, is
[Custody](https://github.com/Himansh97/custody).

## What is here

```
financial-chatbot.ipynb   extraction, analysis and the chat loop
financial-chatbot.html    rendered notebook, readable without running anything
```

Built with Python and pandas. Open the `.html` to read it; run the `.ipynb` to
work with it.

## Limits

Handles the filings it was built against, with a fixed question set. It does not
generalise to arbitrary filings, and the rule-based extraction is tied to the
statement structures it was written for — which is the honest trade for not
letting a model invent the numbers.
