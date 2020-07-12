# Jarvis
# -*- coding: utf-8 -*-
"""
Infant version of something like Siri on iPhone.
I don't have a microphone and so I'm texting in
the shell and it will do it for me. It does speak!!
You can import pyaudio by downloading it using online
sourses or typing on cmd "pip3 install pyaudio" if you
have a microphone. This program greets you, tells you 
today's date and current time and asks you to type 
something in the shell and it will search within your
computer for it and if it does not find it there, it will
look it up online. You can set a default browser as well, like
I set google chrome and search anything online and in your phone.
This is a base model. I can later share how to email someone using 
this or any other advanced functions. Thank You.

"""

import os
import datetime
import playsound
import speech_recognition as sr
from gtts import gTTS
import webbrowser
import pyttsx3

def speak(text):

''' Makes the computer speak. Default voice will be Microsoft Zira Pro '''

    tts = gTTS(text=text, lang="en-us")
    filename = "anyname.mp3"
    tts.save(filename)
    playsound.playsound(filename)	
    os.remove(filename) 		# Removal of the file is necessary because you can't have two different values at the same memory location in the system

def clock():

''' Answers the current time in << hours:minutes:seconds >> format '''

    t = datetime.datetime.now()		# Now is a method in the datetime class in the datetime module that counts time in milliseconds from a particular time till now.
    x = t.strftime("%H:%M:%S")		# Converting milliseconds to H:M:S format.
    return x

def day():

''' Returns today's date as << Day:Month:Date:Year >> format. '''

    t = datetime.datetime.now()
    x = t.strftime("%A, %B %d,%Y")	# Similar to strftime in the previous function, this one will also do conversion but in terms of M:D:Y, A returns the day's name, B returns the name of the month, d returns the date and Y wil obviously give the year.
    return x
    # return datetime.date.today()	# This is an easier method to do the same thing mentioned above as the today method will do this conversion automatically.

def shell():

''' Calling user input ans sending it to your system to look it up within and if not found within, it will go online. '''

    z = input()
    system(z)
    
def system(z):

''' Accessing the system. I just mentioned a few attributes that an average person might use on a regular basis. You can always add more or less. Bonus feature: Shutting down computer. '''

    if z == "shutdown":
        speak("Good Night Boss! I think I'll need some rest now.")
        os.system("shutdown /s /t 0")
    elif z == "word":
        os.startfile("c:\\Users\\USERNAME\\Desktop\\Word")
    elif z == "ppt":
        os.startfile("c:\\Users\\USERNAME\\Desktop\\PowerPoint")
    elif z == "xl":
        os.startfile("c:\\Users\\USERNAME\\Desktop\\Excel")
    elif z == "control":
        os.startfile("C:\\Users\USERNAME\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\System Tools\ Control Panel")
    elif z == "run":
        os.startfile("C:\\Users\USERNAME\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\System Tools\run")
    elif z == "paint":
        os.startfile("C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Accessories\Paint")
    elif z == "snip":
        os.startfile("C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Accessories\Snipping Tool")
    elif z == "media":
        os.startfile("C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Accessories\Windows Media Player")
    elif z == "wordpad":
        os.startfile("C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Accessories\WordPad")
    elif z == "notepad":
        os.startfile("C:\\Users\USERNAME\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Accessories")
    elif z == "explorer":
        os.startfile("C:\\Users\USERNAME\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Accessories\ Internet Explorer")
    elif z == "edge":
        os.startfile("C:\\Users\USERNAME\Desktop\Microsoft Edge")
    elif z == "cmd":
        os.startfile("C:\Windows\System32\cmd.exe")
    elif z == "offline":
        os.startfile("c:\\Users\\USERNAME\\Downloads")
    elif z == "Desktop":
        os.startfile("C:\\Users\\USERNAME\\Desktop")
    elif z =="vlc":
        os.startfile("C:\ProgramData\Microsoft\Windows\Start Menu\Programs\VideoLAN\VLC media player")
    elif z == "other":
        os.startfile("C:\\Users\USERNAME\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\System Tools\File Explorer")
    elif z == "control alter delete":
        os.startfile("C:\ProgramData\Microsoft\Windows\Start Menu\Programs\System Tools\Task Manager")
    else:
        internet(z)

def internet(z):

''' Looks up stuff online when not accessible within the system. I have also set up a default browser over here by the "register" method of webbrowser. You can set any browser similarly
    and changing the address accordingly. I opened gmail and youtube here and everything else will automatically be looked up because I tried to make it more generic. Here's a thing though,
    this google search in the else block will search on a guest google or a non signed in chrome, search anything on google and append to "{}" in the url, everything from the "&" to the "utf-8" encoding, that 
    specifies in the url to search from your google account and remove the ".tr" from the url. Then, it will automatically search on your signed in google chrome for anything which is not on your system as well
    as not gmail or youtube. '''

    webbrowser.register("chrome", None, webbrowser.BackgroundBrowser("C://Program Files (x86)//Google//Chrome//Application//chrome.exe"))
    str(z)
    z.lower()
    if z == "youtube":
        webbrowser.open("http://www.youtube.com")
    elif z == "gmail":
        webbrowser.open("https://mail.google.com/")
    # elif z == "net":
    #    webbrowser.open("C://Program Files (x86)//Google//Chrome//Application//chrome.exe") 
    else:
        webbrowser.open("https://www.google.com.tr/search?q={}".format(z))
      
z = clock()
y = str(day())
speak("Hi Boss! This is Zira, your virtual assistant slash this computer system's jarvis! Today is " + y + "And the time is " + z + "! What can I do for you today? Please type it in the shell")
shell()

def convert():

''' Change the voice and get details. Source geeksforgeeks'''

     converter = pyttsx3.init()
     voices = converter.getProperty('voices')
     for voice in voices:
         print("Voice:") 
         print("ID: %s" %voice.id) 
         print("Name: %s" %voice.name) 
         print("Age: %s" %voice.age) 
         print("Gender: %s" %voice.gender) 
         print("Languages Known: %s" %voice.languages)
