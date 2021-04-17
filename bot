import os
import requests

url = "https://api.telegram.org/bot..token../"

def last_update(request):
  response = requests.get(request + "getUpdates")
  response = response.json()
  results = response["result"]
  total_updates = len(results) - 1
  return results[total_updates]

def get_chat_id(update):
  chat_id = update["message"]["chat"]["id"]
  return chat_id

def get_message_text(update):
  message_text = update["message"]["text"]
  return message_text

def send_message(chat, text):
  params = {"chat_id": chat, "text": text}
  response = requests.post(url + "sendMessage", data=params)
  return response

def connect_net(url):
  try:
    requests.get(url)
    return True
  except:
    return False

def main():
  update_id = last_update(url)["update_id"]
  while 1:
    try:
      update = last_update(url)
      if update_id == update["update_id"]:
        if get_message_text(update).lower() == "hi":
          send_message(get_chat_id(update), "Hello!")
        elif get_message_text(update).lower() == "shutdown":
          send_message(get_chat_id(update), "SHUT...")
          os.system("shutdown -s -t 5")
        else:
          send_message(get_chat_id(update), "I don't understand you!")
        update_id += 1
          
    except:
        break

if __name__ == '__main__':
  while 1:
    if connect_net(url):
     # print("connected")
      main()
