# Lagos & Abuja Rent Predictor

## What problem does this solve?

If you're looking to rent a house in Lagos or Abuja, it's hard to know if a
price is fair. Is ₦4,500,000 a year a good deal for a 3-bedroom flat in
Ikeja, or is someone trying to overcharge you? Most renters have no easy
way to check they just have to guess, or ask around.

This project builds a tool that looks at a house's details (how many
bedrooms, what area it's in, how big it is, etc.) and predicts what the
rent *should* roughly be. Think of it like a price-checker for rent,
similar to how you might check if a phone price on Jumia looks fair based
on what similar phones cost.

## How does it work?

1. **Start with a big list of houses and their rent prices.**
   Each house has details attached to it: which area it's in (e.g. Lekki,
   Wuse 2), how many bedrooms and bathrooms it has, how big it is in
   square meters, whether it's furnished, and so on.

2. **Clean up the list.**
   Some entries were missing details (like the size of the house), and a
   few had impossible prices (like a negative rent, which can't be real).
   Those get fixed or removed before anything else happens.

3. **Turn words into numbers.**
   Computers can't understand words like "Lekki" or "furnished" directly
   they only understand numbers. So each area, property type, and yes/no
   detail gets turned into a simple number code the computer can work with.

4. **Split the list in two.**
   80% of the houses are used to *teach* the computer. The other 20% are
   kept hidden those are used later as a "test" to see if the computer
   actually learned the pattern, or if it's just guessing.

5. **Teach the computer to spot patterns.**
   This is where the "machine learning" happens. The computer looks at
   thousands of examples of "these features this price" and works out
   its own rules for how features connect to price. For example, it might
   notice on its own that houses in Ikoyi tend to cost more than houses in
   Festac, without anyone telling it that directly.

6. **Test it on houses it's never seen.**
   Using the 20% of houses set aside earlier, we ask the computer to guess
   the rent and then compare its guess to the real price, to see how
   close it got.

## Which model did we use, and how good is it?

We tried two different approaches:

| Model | Average mistake (in Naira) | How much it explains |
|---|---|---|
| Linear Regression (simple, straight-line guesser) | ₦941,691 off, on average | 84.9% |
| **Random Forest (final choice)** | **₦527,603 off, on average** | **96.3%** |

**We went with Random Forest** because it was almost twice as accurate.

**What do these numbers actually mean?**
- **₦527,603 average mistake**  if a house's real rent is ₦5,000,000,
  the model's guess is typically somewhere between about ₦4.47M and
  ₦5.53M. Not perfect, but close enough to be a genuinely useful
  starting benchmark.
- **96.3% explained** think of this like a score out of 100 for how
  well the model "gets" what drives rent prices in the data. 96.3 is a
  strong score it means the model is picking up on real, consistent
  patterns, not just guessing randomly.

## What decides the price, based on what the model learned?

Location, property type, and size have the biggest effect on price 
similar to how, in real life, a 3-bedroom flat in Ikoyi will almost
always cost more than the same size flat in Festac, purely because of
where it is.

## What this tool is (and isn't)

This tool gives a **benchmark**, not a guarantee. It's meant to help
someone spot if an asking price is way out of line with similar houses
not to be treated as the exact "correct" rent for every single house.
Real-world prices can also depend on things not captured in this data,
like how new the building is, how the landlord negotiates, or the exact
street it's on.

## Tech used

- **Python** — the programming language
- **pandas** — for loading and cleaning the data
- **scikit-learn** — for building and testing the prediction models
- **Jupyter/Google Colab** — where the code was written and run

## How to run this yourself

1. Open the notebook (`.ipynb` file) in Jupyter or Google Colab.
2. Run each cell from top to bottom, in order.
3. The final cells will print out the model's average error and how
   well it performs, along with example predictions vs actual prices.
