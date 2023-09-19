# VIRTUAL_ASSISTANT
import speech_recognition as sr
import pyttsx3

def listen():
    recognizer = sr.Recognizer()
    with sr.Microphone() as source:
        print("Listening...")
        recognizer.adjust_for_ambient_noise(source, duration=1)
        audio = recognizer.listen(source)

    try:
        print("Recognizing...")
        user_input = recognizer.recognize_google(audio).lower()
        print("You said:", user_input)
        return user_input
    except sr.UnknownValueError:
        print("Sorry, I didn't catch that.")
        return ""
    except sr.RequestError:
        print("Sorry, I'm having trouble with speech recognition.")
        return ""

def speak(text):
    engine = pyttsx3.init()
    engine.say(text)
    engine.runAndWait()

def virtual_assistant():
    speak("Hello! I'm your virtual assistant. How can I assist you today?")
    
    while True:
        user_input = listen()
        
        if "hello" in user_input:
            speak("Hello! How can I help you?")
        elif "what's your name" in user_input:
            speak("I am your virtual assistant.")
        elif "goodbye" in user_input:
            speak("Goodbye! Have a great day.")
            break
        else:
            speak("I'm sorry, I didn't understand that.")

if __name__ == "__main__":
    virtual_assistant()
