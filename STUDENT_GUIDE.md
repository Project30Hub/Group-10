# Blackjack Project: Student Learning Guide

This folder is designed for a student who is just starting to learn Python. Each section explains not only the "what" but the "how" and "why" of the Python language.

## 1. The Problem: What are we building?

In simple terms, we are building a "Rule Book" for a game of Blackjack.

Imagine you are teaching a computer how to play. The computer doesn't know what a "card" is or what "hit" means. We have to give it:

1. **Data**: (What cards are on the table?)
2. **Logic**: (If you have two 8s, you are allowed to Split).
3. **Changes**: (If you "Hit", you add a card to your hand).

---

## 2. Input, Process, and Output (The "Pipeline")

### Input (The Raw Material)

The program receives a **String**. In Python, a string is just text inside quotes.

- *Example:* `"10,6 | 9 | first"`
- We need to break this string apart to understand it.

### Process (The Brains)

The program does three main things:

1. **Parsing**: Breaking the text into a **List** (like a shopping list) and a **Dictionary** (like a real dictionary where a "key" leads to a "value").
2. **Checking Rules**: Using `if` statements to see if an action is allowed.
3. **Updating**: Changing the list of cards when a player takes an action.

### Output (The Result)

The program gives back either:

- A **List of Strings** (e.g., `["Hit", "Stand", "Split"]`)
- A **List of Cards** (e.g., `["10", "6", "2"]`)

---

## 3. Step-by-Step Logic (Pseudocode)

*Pseudocode is just writing logic in English before we translate it into "Computer Language" (Python).*
IF the turn stage is "first":
    ADD "Double Down" and "Surrender" to the list

    IF the first card rank is the same as the second card rank:
        ADD "Split" to the list (because they are a pair!)

    IF the dealer's card is an "A" (Ace):
        ADD "Insurance" to the list

RETURN the final list of moves
---

## 4. How the Code Works (For Beginners)

Here is the breakdown of the Python concepts used in this project:

### A. Dictionaries (`{}`)

We use a dictionary called `RANK_VALUES`.

- **Why?** Because "J", "Q", and "K" aren't numbers. A dictionary lets us say: "If you see a 'K', treat it as the number 10."

### B. Lists (`[]`)

The player's hand is stored as a list: `['10', '6']`.

- **Why?** Lists are great because we can easily `.append()` (add) a new card to the end of the list when the player "Hits".

### C. The `if` Statement

We use `if` and `elif` (else if) to make decisions.

- *Example:* `if state['stage'] == "first":`
- This tells Python: "Only do the next bit of code if this specific condition is true."

### D. Loops (`while`)

In the `hand_value` function, we use a `while` loop.

- **Why?** Because a player might have multiple Aces. The loop keeps subtracting 10 from the total as long as the score is over 21 AND there are still Aces to change from 11 to 1.

---

## 5. Flowchart Connection

If you look at a flowchart:

- **Ovals** = The start and end of the program.
- **Parallelograms** = Getting a string or printing a result (Input/Output).
- **Rectangles** = Doing a calculation or changing a variable (Process).
- **Diamonds** = An `if` statement (Decision).
