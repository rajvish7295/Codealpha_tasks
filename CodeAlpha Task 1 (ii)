import speech_recognition as sr
import pyttsx3
import datetime
import webbrowser
import os


engine = pyttsx3.init()

voices = engine.getProperty('voices')
engine.setProperty('voice', voices[0].id)  # Use the first voice
engine.setProperty('rate', 150)  # Set the speaking rate

def speak(text):

    engine.say(text)
    engine.runAndWait()

def listen():

    recognizer = sr.Recognizer()
    with sr.Microphone() as source:
        print("Listening...")
        recognizer.adjust_for_ambient_noise(source, duration=1)
        try:
            audio = recognizer.listen(source, timeout=10)
            command = recognizer.recognize_google(audio)
            print(f"You said: {command}")
            return command.lower()
        except sr.UnknownValueError:
            speak("Sorry, I couldn't understand that. Please say it again.")
            return ""
        except sr.RequestError:
            speak("Sorry, my speech recognition service is unavailable.")
            return ""
        except Exception:
            speak("Listening timed out.")
            return ""

def greet_user():
    """Greet the user based on the time of day."""
    hour = datetime.datetime.now().hour
    if 0 <= hour < 12:
        speak("Good morning!")
    elif 12 <= hour < 18:
        speak("Good afternoon!")
    else:
        speak("Good evening!")
    speak("How can I assist you today?")

def perform_task(command):
    """Perform tasks based on the voice command."""
    if "time" in command:
        current_time = datetime.datetime.now().strftime("%I:%M %p")
        speak(f"The current time is {current_time}")
    elif "open browser" in command:
        speak("Opening the web browser.")
        webbrowser.open("https://www.google.com")
    elif "open facebook" in command:
        speak("Opening the facebook")
        webbrowser.open("https://www.facebook.com")
    elif "open instagram" in command:
        speak("Opening the instagram")
        webbrowser.open("https://www.instagram.com")
    elif "play music" in command:
        music_dir = "C:/Users/Public/Music/raj music"
        songs = os.listdir(music_dir)
        if songs:
            speak("Playing music.")
            os.startfile(os.path.join(music_dir, songs[0]))
        else:
            speak("No music found in the specified directory.")
    elif "shutdown" in command:
        speak("Shutting down. Have a nice day!")
        exit()
    else:
        speak("Sorry, I didn't understand that command. Please try again.")

# Main Program
if __name__ == "__main__":
    speak("Initializing your personal assistant.")
    greet_user()

    while True:
        command = listen()
        if command:
            perform_task(command)
