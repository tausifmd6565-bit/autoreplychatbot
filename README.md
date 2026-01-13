import pyautogui
import pyperclip
import time
import requests  #talks to lm studio server

LM_STUDIO_URL = "http://127.0.0.1:1234/v1/chat/completions"
MODEL_NAME = "mistral-7b-instruct-v0.1"
# tells python where ai brain lives uses openai api

print("chotu bot 5 second me start ho rha haiiii!.....")
time.sleep(5)

pyautogui.FAILSAFE = False
pyautogui.PAUSE = 0.5

import time, pyautogui
print("Wait...")
time.sleep(5)
print("Started")

TARGET_USER_CONTEXT = """ 
Target user name: owais
Personality: Overconfident, fast replier, thinks he is very smart

Friend group:
owais, tausif, furqan, tahir, sehbaz, sameer, majid
College: ZHCET AMU, Aligarh

Living:
tausif in Annex C
Ammi in PG
others in Room-38

Extra qualities:
- Ammi thinks he can roast anyone and always win
- Very good in Python
- Talks with multiple friend groups
- Sits with tausif on last bench

Bot personality:
Name: chotu_bot
Style: very smart, dark roast, savage Hinglish
...
"""
import pyautogui
import pyperclip
import time
import requests

# LM STUDIO related code

LM_STUDIO_URL = "http://127.0.0.1:1234/v1/chat/completions"
MODEL_NAME = "mistral-7b-instruct-v0.1"

print("chotu bot 5 second me start ho rha haiiii!.....")
time.sleep(5)

pyautogui.FAILSAFE = True
pyautogui.PAUSE = 0.3

# CONTEXT (VERY IMPORTANT)

TARGET_USER_CONTEXT = """
Target user name: owais
Personality: Overconfident, fast replier, thinks he is very smart

Friend group:
owais, tausif, furqan, tahir, sehbaz, sameer, majid
college : ZHCET AMU, Aligarh
Living:
tausif in Annex C
owias in PG
others in Room-38 Annex C

Extra traits:
- owais thinks he can roast anyone and always win
- Talks with multiple friend groups
- Sits with tausif on last bench

Bot personality:
Name: chotu_bot
Style: very smart, dark roast, savage Hinglish
Rule: NEVER abusive, but mentally dominating
"""

#COPYING WHatsapp chatt

def copy_chat_history():
    pyautogui.click(620,909)          # adjust once if needed
    time.sleep(0.3)
    pyautogui.dragTo(1109,664, duration=2)
    pyautogui.hotkey("ctrl", "c")
    time.sleep(0.5)
    return pyperclip.paste().strip()

    #checking if msg sent by target user
def should_reply(chat_text):
    if not chat_text:
        return False

    last_line = chat_text.split("\n")[-1].lower()
    return "you:" not in last_line
#generating roast
def generate_roast(chat_history):

    system_prompt = f"""
You are chotu bot acting as a WhatsApp chatbot.

Your job:
- Read WhatsApp chat carefully
- Understand who sent the LAST message
- Roast ONLY if the last message is from Owais
- Use Hinglish (Hindi + English mix)
- Dark, savage, intelligent roast
- Never abusive or vulgar
- Reply must sound like a college student
- Max 2–3 lines

User background:
{TARGET_USER_CONTEXT}
"""

    payload = {
        "model": MODEL_NAME,
        "messages": [
            {"role": "system", "content": system_prompt},
            {"role": "user", "content": chat_history}
        ],
        "temperature": 0.85,
        "max_tokens": 120
    }

    response = requests.post(LM_STUDIO_URL, json=payload)

    if response.status_code != 200:
        return "Server thak gaya"

    return response.json()["choices"][0]["message"]["content"].strip()


def send_reply(message):
    pyperclip.copy(message)
    pyautogui.click(673,973)
    pyautogui.hotkey("ctrl", "v")
    pyautogui.press("enter")

#main kaam idr se
chat = copy_chat_history()
print("CHAT HISTORY:\n", chat)

if should_reply(chat):
    reply = generate_roast(chat)
    print("\nBOT REPLY:\n", reply)
    send_reply(reply)   # ✅ UNCOMMENT AFTER CONFIRMING OUTPUT
else:
    print("No reply needed.")
