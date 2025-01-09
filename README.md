from http import server
import speech_recognition as sr
"Subject: {subject}\n\n{message}"
server.sendmail("your_email@gmail.com", to, email_message)
server.close()
speak("Email sent successfully.")
try:
    # Code that might raise an exception
    server.sendmail("your_email@gmail.com", to, email_message)
except Exception as e:
    # Handle the exception
    print(f"An error occurred: {e}")
speak("I couldn't send the email.")

# Alarm Functionality
def set_alarm(alarm_time):
    while True:
        current_time = time.strftime("%H:%M:%S")
        if current_time == alarm_time:
            speak("Time to wake up!")
            break
        time.sleep(1)

# Solve Math Expression
def solve_expression(expression):
    try:
        result = simplify(expression)
        speak(f"The result is {result}")
    except Exception:
        speak("I couldn't solve the expression.")

# Personalized Greeting
def personalized_greeting():
    hour = datetime.now().hour
    if hour < 12:
        speak("Good morning!")
    elif 12 <= hour < 18:
        speak("Good afternoon!")
    else:
        speak("Good evening!")

# Assistant Response
def assistant_response(query):
    if 'wikipedia' in query:
        speak("Searching Wikipedia...")
        query = query.replace("wikipedia", "")
        results = wikipedia.summary(query, sentences=2)
        speak("According to Wikipedia")
        speak(results)

    elif 'open youtube' in query:
        speak("Opening YouTube")
        webbrowser.open("youtube.com")

    elif 'open google' in query:
        speak("Opening Google")
        webbrowser.open("google.com")

    elif 'play music' in query:
        speak("Playing music")
        subprocess.Popen(['start', 'ms-wmp'], shell=True)

    elif 'the time' in query:
        str_time = datetime.now().strftime("%H:%M:%S")
        speak(f"The time is {str_time}")

    elif 'joke' in query:
        joke = pyjokes.get_joke()
        speak(joke)

    elif 'search' in query:
        query = query.replace("search", "")
        speak(f"Searching {query} on Google")
        webbrowser.open(f"https://www.google.com/search?q={query}")

    elif 'ask' in query:
        speak("What is your question?")
        question = take_command()
        client = wolframalpha.Client('YOUR_WOLFRAMALPHA_APP_ID')  # Replace with your App ID
        try:
            res = client.query(question)
            answer = next(res.results).text
            speak(answer)
        except Exception:
            speak("I couldn't find an answer to your question.")

    elif 'weather' in query:
        speak("Which city?")
        city = take_command()
        if city:
            get_weather(city)

    elif 'news' in query:
        get_news()

    elif 'set reminder' in query:
        speak("What should I remind you about?")
        task = take_command()
        if task:
            set_reminder(task)

    elif 'show reminders' in query:
        list_reminders()

    elif 'send email' in query:
        speak("To whom should I send the email?")
        to = take_command()
        speak("What is the subject?")
        subject = take_command()
        speak("What is the message?")
        message = take_command()
        if to and subject and message:
            send_email(to, subject, message)

    elif 'set alarm' in query:
        speak("What time should I set the alarm for? (in HH:MM:SS format)")
        alarm_time = take_command()
        if alarm_time:
            set_alarm(alarm_time)

    elif 'solve' in query:
        speak("Please state the math expression.")
        expression = take_command()
        if expression:
            solve_expression(expression)

    elif 'quit' in query or 'exit' in query:
        speak("Goodbye!")
        exit()

    else:
        speak("I didn't understand. Could you say that again?")

# Main Function
def main():
    personalized_greeting()
    speak("Hello! How can I assist you today?")

    while True:
        query = take_command()
        if query:
            assistant_response(query)

if __name__ == "__main__":
    main()
