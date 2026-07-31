🎓 Student-Friendly Python Implementation: Blackjack
This code is written specifically for students learning Python. I have added "Educational Comments" that explain the Python concepts being used in real-time.

# --- CONCEPT: DICTIONARIES ---
# A dictionary is like a real-life dictionary. 
# The 'Key' (e.g., "K") maps to a 'Value' (e.g., 10).
# We use this so the computer knows how many points a face card is worth.
RANK_VALUES = {
    "2": 2, "3": 3, "4": 4, "5": 5, "6": 6, "7": 7, "8": 8, "9": 9, "10": 10,
    "J": 10, "Q": 10, "K": 10, "A": 11,
}

def hand_value(cards):
    \"\"\"
    This function calculates the total score of a hand.
    \"\"\"
    # --- CONCEPT: LIST COMPREHENSION ---
    # This fancy line tells Python: "Look at every card in the hand list, 
    # find its number in RANK_VALUES, and sum them all up."
    total = sum(RANK_VALUES[card] for card in cards)
    
    # We count how many Aces ('A') are in the hand.
    aces = cards.count("A")
    
    # --- CONCEPT: WHILE LOOP ---
    # A 'while' loop keeps running as long as the condition is TRUE.
    # If the total is over 21 and we have an Ace, we treat the Ace as 1 instead of 11.
    # We subtract 10 from the total and decrease our Ace count by 1.
    while total > 21 and aces > 0:
        total -= 10
        aces -= 1
    return total

def parse_state(text):
    \"\"\"
    This function takes a piece of text and turns it into a Python Dictionary.
    Example: "10,6 | 9 | first" -> {'hand': ['10', '6'], ...}
    \"\"\"
    # --- CONCEPT: STRING SPLITTING ---
    # .split("|") cuts the text into a list wherever it sees a '|' symbol.
    # .strip() removes any accidental spaces at the start or end of the text.
    parts = [part.strip() for part in text.split("|")]
    
    hand_str = parts[0]      # The first part: "10,6"
    dealer_upcard = parts[1] # The second part: "9"
    flag = parts[2]          # The third part: "first"
    
    # We split the hand_str by the comma to get a list of individual cards.
    hand = [rank.strip() for rank in hand_str.split(",")]
    
    # We return a Dictionary. This allows us to access data using names like state['hand'].
    return {"hand": hand, "dealer": dealer_upcard, "stage": flag}

def generate_actions(state):
    \"\"\"
    This function acts as the 'Rule Book' to decide what the player can do.
    \"\"\"
    # --- CONCEPT: LISTS ---
    # We start with a list. Every player can always 'Hit' or 'Stand'.
    actions = ["Hit", "Stand"]
    
    # --- CONCEPT: IF STATEMENTS (CONDITIONS) ---
    # We check if this is the 'first' decision of the turn.
    if state['stage'] == "first":
        # .extend() adds multiple items to our list at once.
        actions.extend(["Double Down", "Surrender"])
        
        # Rule: You can only 'Split' if you have exactly 2 cards and they are the same.
        # state['hand'][0] is the first card, state['hand'][1] is the second.
        if len(state['hand']) == 2 and state['hand'][0] == state['hand'][1]:
            actions.append("Split") # .append() adds one single item to the list.
            
        # Rule: Insurance is only an option if the dealer is showing an Ace.
        if state['dealer'] == "A":
            actions.append("Insurance")
            
    return actions

def apply_action(state, action, next_card=None):
    \"\"\"
    This function changes the game state based on the action chosen.
    \"\"\"
    # We use if/elif to handle different actions.
    if action == "Hit":
        # Add the new card to the end of the hand list.
        state['hand'].append(next_card)
        
        # IMPORTANT: Once you hit, it is no longer your 'first' decision.
        # We change 'first' to 'later' so the player can't Split or Double next time.
        state['stage'] = "later"
        return state['hand']
    
    elif action == "Split":
        # --- CONCEPT: NESTED LISTS ---
        # Splitting creates TWO hands. In Python, we represent this as a list 
        # containing two other lists: [[card1], [card2]].
        first_card = state['hand'][0]
        second_card = state['hand'][1]
        return [[first_card], [second_card]]
    
    # If the action was 'Stand' or 'Insurance', the cards don't change.
    return state['hand']
