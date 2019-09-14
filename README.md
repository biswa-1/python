# python
import datetime
import pyttsx3
import wikipedia
import random
import os
import webbrowser
import speech_recognition as sr
engine = pyttsx3.init('sapi5')
voices = engine.getProperty('voices')
# print(voices[0].id)
engine.setProperty('voices', voices[0].id)
def speak(audio):
    engine.say(audio)
    engine.runAndWait()
def wish_me():
    hour = int(datetime.datetime.now().hour)
    if hour >= 0 and hour <= 12:
        speak("good mourning Biswajit")
    elif hour >= 12 and hour <= 18:
        speak("good after noon")
    else:
        speak("good evening")
    speak("i am  your vector, please tell me how may i help you")
    # print(hour)
def takecommand():
    r = sr.Recognizer()
    with sr.Microphone() as source:
        print("Listening....")
        r.pause_threshold = 1
        audio = r.listen(source)
    try:
        print("Recognize...")
        query = r.recognize_google(audio, language='en-in')
        print(f'user said: {query}\n')
    except Exception as e:
        # print(e)
        print("say that again plz")
        return "None"
    return query



if __name__ == "__main__":
    wish_me()
    while True:
        query = takecommand().lower()
        if 'wikipedia' in query:
            speak("searching wikipedia....")
            query = query.replace("wikipedia", "")
            results = wikipedia.summary(query, sentences=4)
            speak("According to wikipedia...")
            print(results)
            speak(results)
        elif "open google" in query:
            webbrowser.open("google.com")
        elif "open facebook" in query:
            webbrowser.open("facebook.com")
        elif "open gaana" in query:
            webbrowser.open("gaana.com")
        elif "open youtube" in query:
            webbrowser.open("youtube.in")
        elif "play songs" in query:
            music_dir = "D:\\music"
            songs = os.listdir(music_dir)
            os.startfile(os.path.join(music_dir, random.choice(songs[0])))
        elif "the time" in query:
            strtime = datetime.datetime.now().strftime("%H:%M:%S")
            print(strtime)
            speak(f"sir, The time is{strtime}")
        elif "open code" in query:
            codepath = "C:\\Users\\pradh\\AppData\\Local\\Programs\\Microsoft VS Code\\Code.exe"
            os.startfile(codepath)
