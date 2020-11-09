# YUG-THE-AI-DESKTOP-VOICE-ASSISTANT-
I have made this project considering the Real world comfort. 
I have used the VS code IDE. 
To make "YUG" speak I have used function called speak().
To convert text to speech I used pyttsx3().Then I installed "sapi5" an speech API developed by Microsoft helps to recognition the voice. created a main fn() inside which i have called my speech().
To initialize my take command I have installed "speech recognition" .Then used several "if-else" ladder for performing multiple search operations.
Apart from this, if you asked for any query which has not been programmed there, then it will take it as an exception.

************************************************************Source code*******************************************************************************


import pyttsx3
import datetime
import speech_recognition as sr
import pyaudio
import wikipedia
import webbrowser
import os
import smtplib


engine = pyttsx3.init('sapi5')
voices = engine.getProperty('voices')
print(voices[0].id)
engine.setProperty('voice', voices[0].id)


def speak(audio):
    pass
    engine.say(audio)
    engine.runAndWait()


def wishMe():
    hour = int(datetime.datetime.now().hour)
    if hour>=0 and hour<=12:
        speak("GOOD MORNING MUDIT")
        speak("YUG IS HERE SIR, HOW MAY I HELP YOU")

    elif hour>= 12 and hour<=16:
        speak("GOOD AFTERNOON MUDIT")
        speak("YUG IS HERE SIR, HOW MAY I HELP YOU")


    elif hour>=16 and hour<=20:
        speak("GOOD EVENING MUDIT")
        speak("YUG IS HERE SIR , HOW MAY I HELP YOU ")

    else:
        speak("OHH Shocked to see you awake") 
        speak("Anyways, HOW MAY I HELP YOU")   


def takeCommand():
        # It takes microphone input from the user and returns string output

        r = sr.Recognizer()
        with sr.Microphone() as source:
            print("Listening...")
            r.pause_threshold = 1
            r.energy_threshold = 50
            audio = r.listen(source)

        try:
            print("Recognizing...")
            query = r.recognize_google(audio, language='en-in')
            print(f"User said: {query}\n")

        except Exception as e:
            print(e)
            print("Say that again please...")
            return "None"
        return query


def sendEmail(to, content):
    server = smtplib.SMTP('smtp.gmail.com', 587)
    server.ehlo()
    server.starttls()
    server.login('mudit*******gmail.com', 'password-here')
    server.sendmail('youremail@gmail.com', to, content)
    server.close()




if __name__ == '__main__':
 wishMe()
 while True:
        query = takeCommand().lower()
        #logics for executing tasks based on query
        if 'wikipedia' in query:
                speak('searching wikipedia...')
                query = query.replace("wikipedia","")
                results = wikipedia.summary(query, sentences=2)
                speak('According to wikipedia')
                print(results)
                speak(results)


        elif 'open youtube' in query:
          webbrowser.open('youtube.com')

        elif 'open NASA' in query:
          webbrowser.open('https://www.nasa.gov/')

        elif 'open ISRO' in query:
          webbrowser.open('https://www.isro.gov.in/')

        elif 'tell me the time' in query:
          strTime = datetime.datetime.now().strftime("%H:%M:%S")
          speak(f'Sir,the time is {strTime} , hope you are doing well')
          print(f'Sir,the time is {strTime} , hope you are doing well')

        elif 'open narcos' in query:
         codePath ="D:\\tv series\\Narcos\\Season-1"
         os.startfile(codePath)

        elif 'email to Mudit' in query:
         try:
             speak("What should I say?")
             content = takeCommand()
             to = "muditsrivastava@gmail.com" # Try writing yours ;)
             sendEmail(to, content)
             speak("Email has been sent!")
         except Exception as e:
             print(e)
             speak("Sorry, but i could not sent this email")

      
        
        elif 'awesome YUG' in query or 'wow' in query or 'amazing' in query or 'wonderful' in query:
            speak("Thank you sir, i am here for you")
            print("Thanks you sir , i am here for you")

        elif 'what' in query or 'who' in query or 'where' in query or 'can you' in query:
            webbrowser.open(f"https://www.google.com/search?&q={query}")
            speak(wikipedia.summary(query, sentences=2))
              
         
        elif 'news today' in query:
             speak('here is your news sir')
             webbrowser.open('https://www.hindustantimes.com/')
             print("enjoy..")


        elif 'YUG quit' in query or 'exit YUG' in query or 'close' in query:
            speak("Thanks for using YUG!!!")
            print("Thanks for using YUG!!")
            exit()
               
