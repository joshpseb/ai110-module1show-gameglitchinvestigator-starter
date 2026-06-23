# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

When I first ran the game it looked normal, but when I started playing the hints were telling me to go in the wrong direction, my score went up after a wrong guess, and the description for hard mode was different in different places.

The two biggest bugs I noticed right away were the inverted hints and the weird scoring. The difficulty range bug took a minute to spot because I had to switch modes and read the sidebar.

Bug Reproduction Log

| Input Used | Expected Behavior | Actual Behavior | Console Output / Error |
|------------|-------------------|-----------------|------------------------|
| Guess of 80 when secret is 42 | "Go LOWER!" since the guess is too high | "Go HIGHER!" shown — the hint messages are swapped in the code | none |
| Made a wrong guess | Score goes down | score goes up | none |
| Select Hard difficulty | A harder range like 1 to 200 or higher, or less attempts | Sidebar shows range 1 to 50, which is easier than Normal's 1 to 100 | none |

---

## 2. How did you use AI as a teammate?

I used Cursor's AI (Claude) with the project files attached so it could see both app.py and logic_utils.py at the same time.

One thing the AI got right was spotting that the hint messages in check_guess were swapped. I described the issue: guessing high and being told to go higher, and the AI immediately pointed to the lines where "Go HIGHER!" and "Go LOWER!" were on the wrong branches. I verified it by running the two new pytest cases, which passed after the fix.

One thing the AI got wrong was that it initially left the old check_guess definition in app.py when adding the import from logic_utils, which caused a conflict where the local version overrode the imported one. I caught it by reading the diff carefully and asked for a targeted correction to remove the leftover definition.

---

## 3. Debugging and testing your fixes

I decided a bug was fixed when I could run pytest and see the relevant test pass, and then also play the game manually and get a hint that made sense given my guess.

One test I ran calls check_guess(80, 42) and asserts that "LOWER" is in the message. Before the fix that test would have failed because the message said "Go HIGHER!" even when the guess was too high. After moving the corrected function into logic_utils.py and running pytest, all five tests passed. That gave me more confidence than just eyeballing the code because it locked in the exact behavior I expected.

The AI helped me think of what to assert. I told it I wanted to test the hint direction bug specifically and it suggested checking the message string for "LOWER" or "HIGHER" instead of comparing the full string.

---

## 4. What did you learn about Streamlit and state?

Every time you interact with anything in a Streamlit app the entire script reruns from top to bottom. That means any regular variable you set gets thrown away on the next interaction. Session state is basically a dictionary that continues through those reruns, so if you store the secret number or the attempt count there, it stays instead of resetting every time the user clicks something.

---

## 5. Looking ahead: your developer habits

I want to keep up the habit of creating a new chat session for every issue, since it helps the AI focus on a sole task without being distracted by outside elements.

Next time I'd give the AI a more specific prompt upfront instead of describing the bug vaguely and then correcting it in follow-ups. The more context I gave like pasting the exact line and explaining what I expected versus what happened the faster it landed on the right fix.

It's important to not take everything AI gives you as being perfect. Reviewing AI code and implementing it is even more important in order to get a real understanding and to make sure things are being done correctly.