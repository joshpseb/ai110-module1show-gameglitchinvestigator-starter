# 🎮 Game Glitch Investigator: The Impossible Guesser

## 🚨 The Situation

You asked an AI to build a simple "Number Guessing Game" using Streamlit.
It wrote the code, ran away, and now the game is unplayable. 

- You can't win.
- The hints lie to you.
- The secret number seems to have commitment issues.

## 🛠️ Setup

1. Install dependencies: `pip install -r requirements.txt`
2. Run the broken app: `python -m streamlit run app.py`

## 🕵️‍♂️ Your Mission

1. **Play the game.** Open the "Developer Debug Info" tab in the app to see the secret number. Try to win.
2. **Find the State Bug.** Why does the secret number change every time you click "Submit"? Ask ChatGPT: *"How do I keep a variable from resetting in Streamlit when I click a button?"*
3. **Fix the Logic.** The hints ("Higher/Lower") are wrong. Fix them.
4. **Refactor & Test.** - Move the logic into `logic_utils.py`.
   - Run `pytest` in your terminal.
   - Keep fixing until all tests pass!

## 📝 Document Your Experience

This is a number guessing game built with Streamlit where the player tries to guess a secret number within a limited number of attempts. The difficulty setting controls the range and number of attempts allowed. After each guess the game gives a hint telling you to go higher or lower, and your score changes based on how many guesses it takes to win.

When I first ran the app the hints were backwards — guessing too high told me to go higher, which made it impossible to win by following the hints. On top of that, the score would sometimes go up after a wrong guess depending on which attempt number it was, which made the scoring feel random. The Hard difficulty also had a range of 1 to 50, which was actually easier than Normal's 1 to 100.

I fixed the hint direction bug by correcting the messages inside check_guess, where Go LOWER and Go HIGHER were assigned to the wrong branches. I fixed the score bug by removing a parity check that was rewarding wrong guesses on even-numbered attempts. I also refactored check_guess out of app.py and into logic_utils.py to separate the game logic from the UI code, and added a conftest.py so pytest could find the module.

## 📸 Demo Walkthrough

Describe your fixed game in numbered steps so a reader can follow along without watching a video:

1. User enters a guess of 50
2. Game returns "Too High"
3. User enters a guess of 30 → "Too Low"
4. Score decreases by 5 for every incorrect guess
5. Game ends after the correct guess or guesses run out
6. Score is displayed


## 🧪 Test Results

% pytest
=========================== test session starts ===========================
platform darwin -- Python 3.11.4, pytest-7.4.0, pluggy-1.0.0
rootdir: /Users/joshseb/Downloads/School/CodePath/ai/ai110-module1show-gameglitchinvestigator-starter
plugins: xonsh-0.18.3, anyio-4.13.0
collected 5 items                                                         

tests/test_game_logic.py .....                                      [100%]

============================ 5 passed in 0.02s ============================

## 🚀 Stretch Features

- [ ] [If you choose to complete Challenge 4, describe the Enhanced UI changes here — a screenshot is optional]
