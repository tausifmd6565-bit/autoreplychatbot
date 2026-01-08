# autoreplychatbot
import pyautogui
import pyperclip
import time
#pyautogui is python library that automates and controls mouse and keypad , pyperclip is like copy and paste , time is builtin python function that delays time 

print("chotu roster starting in 5 seconds......")
time.sleep(5)

pyautogui.FAILSAFE = True  #stops if mouse goes to top-left corner needed coz: if automation goes wrong u can stop instantly

def copy_chat_history():
    pyautogui.moveTo(300, 300)
    pyautogui.dragTo(900, 600, duration=2)
    pyautogui.hotkey("ctrl", "c")
    time.sleep(1)
    return pyperclip.paste()

"""moveTo - it moves the mouse to chat area
   dragTo- select message , hotkey - ctrl+c(it elps to contrl shift and fn. command)"""

def is_last_message_from_user(chat_text, username):
    lines = chat_text.strip().split("\n")
    last_line = lines[-1]
    return last_line.startswith(username)
"""1. chat_text.strip().split("\n")
.strip(): Removes any accidental empty spaces or "new line" characters at the very beginning or the very end of the copied text.

.split("\n"): This is the most important part. It takes the big block of chat history (one long string) and cuts it into a List of strings, using every "New Line" (where you pressed Enter) as the cutting point.

2. last_line = lines[-1]
In Python, the index [-1] always grabs the very last item in a list.

Because you just split the chat into lines, lines[-1] represents the most recent message sent in the chat.

3. return last_line.startswith(username)
This checks if the last line begins with the name you are looking for (e.g., "Rohan Das").

If it matches: It returns True (Naruto should roast him!).

If it doesn't: It returns False (Naruto stays silent)."""
def send_reply(message):
    pyperclip.copy(message)
    pyautogui.click(500, 700)
    pyautogui.hotkey("ctrl", "v")
    pyautogui.press("enter")

def generate_fake_roast():
    return "Oi tausif , even Naruto trains harder than you type!"

while True:
    chat = copy_chat_history()

    if is_last_message_from_user(chat, "Rohan"):
        reply = generate_fake_roast()
        send_reply(reply)
        time.sleep(10)

    time.sleep(5)
