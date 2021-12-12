# Speech-to-Speech
import speech_recognition as sr
import pyttsx3
import pywhatkit
import datetime
import wikipedia
import pyjokes
import webbrowser
import os
import smtplib

listener = sr.Recognizer()
engine = pyttsx3.init()
voices = engine.getProperty('voices')
engine.setProperty('voice', voices[0].id)


def talk(text):
    engine.say(text)
    engine.runAndWait()
  
talk('Hi i am AISAC how can i help you')
def take_command():
    try:
        with sr.Microphone() as source:
            print('listening...')
            listener.adjust_for_ambient_noise(source,duration=1)
            voice = listener.listen(source)
            command = listener.recognize_google(voice)
            command = command.lower()
            if 'aisac' in command:
                command = command.replace('aisac', '')
                print(command)
    except:
        pass

    return command


def run_aisac():
    command = take_command()
    print(command)
    if 'play' in command:
        song = command.replace('play', '')
        talk('playing ' + song)
        pywhatkit.playonyt(song)
    elif 'youtube' in command:
        talk('opening youtube')
        webbrowser.open('www.youtube.com')
    elif 'chrome' in command:
        talk('opening Google chrome')
        webbrowser.open('www.google.co.in')
    elif 'whatsapp' in command:
        talk('opening Whatsapp')
        webbrowser.open('https://web.whatsapp.com/')
    elif 'google meet' in command:
        talk('opening Google Meet')
        webbrowser.open('https://meet.google.com/')  
    elif 'zoom meeting' in command:
        talk('opening zoom meeting')
        webbrowser.open('https://zoom.us/')       
    elif 'g mail' in command:
        talk('opening g mail')
        webbrowser.open('https://mail.google.com/')   
    elif 'time' in command:
        time = datetime.datetime.now().strftime('%I:%M %p')
        talk('Current time is ' + time)
    elif 'who is' in command:
        person = command.replace('who is', '')
        info = wikipedia.summary(person, 1)
        print(info)
        talk(info)
    elif 'what is' in command:
        person = command.replace('who is', '')
        info = wikipedia.summary(person, 1)
        print(info)
        talk(info)

    elif 'How are you?' in command:
        talk('I'm good, How are you buddy?')
    elif 'I'm so happy' in command:
        talk('Good to hear, I'm so excited for you, let's celebrate this')
    elif 'do you know my name' in command:
        talk('Hi buddy, how can i forget you, you are my best friend')
    elif 'I'm not doing good, can you help me?' in command:
        talk('Hey buddy don't worry, I'm there for you, you can share anything to me, I'm there for you. Or should I call anyone?')
    elif 'who created you' in command:
        talk('I was created by a team of 4 members name, Hemanth, Sudharsan, Shrinithi, and Karanam Poorna Siri. Their team name is Captain Jack Sparrow lol!')
    elif 'describe about yourself' in command:
        talk('My name is AISAC, i am your close friend and your soul companion. i will be helping you with all your ups and downs, you can share anything to me. I'm your trust worthy friend')
    elif 'joke' in command:
        talk(pyjokes.get_joke())
    else:
        talk('Please say the command again.')


while True:
    run_aisac()
