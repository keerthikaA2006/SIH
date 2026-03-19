## TITLE:
Secure Multi-User Organizational Knowledge Chatbot with Document Processing

## NAME:KEERTHIKA A
## REG NO:212224220048
## Problem Title:
AI-Based Organizational Knowledge Chatbot with Secure Access and Document Processing

## Problem Description:
Large organizations handle a lot of internal information such as HR policies, leave rules, IT support procedures, and employee guidelines. Employees often waste time searching through documents or contacting departments for simple queries.

There is a need for an intelligent system that can automatically answer employee queries, provide organization-related information, and analyze uploaded documents. The system should also ensure security by authenticating users and filtering inappropriate language.

Therefore, an AI-based chatbot can be developed to provide quick access to organizational knowledge while supporting multiple users and basic document analysis.

## Idea / Proposed Solution:
The proposed system is a Python-based AI chatbot that helps employees access internal organizational information easily.

#vKey ideas of the system: A knowledge base stores common organizational information such as leave policies, password reset procedures, and timesheet updates.

Users must pass OTP authentication before accessing the chatbot to ensure security.

The chatbot processes user questions and retrieves answers from the knowledge base.

A bad language filter ensures professional communication.

The system supports multiple users simultaneously using threading.

Users can simulate document uploads, and the system extracts a summary and important keywords.

This solution improves communication efficiency and reduces workload on HR and IT departments.

## Architecture Diagram (Text Representation):
          +----------------------+
             |      Users (1-5)     |
             +----------+-----------+
                        |
                        v
             +----------------------+
             |   OTP Authentication |
             +----------+-----------+
                        |
                        v
             +----------------------+
             |   Input Processing   |
             | (Bad Word Filter)    |
             +----------+-----------+
                        |
         +--------------+--------------+
         |                             |
         v                             v
+-----------------------+        +-----------------------+
|   Knowledge Base      |        |   Document Processor  |
| (Policies, IT Help)   |        | (Summary + Keywords)  |
+-----------+-----------+        +-----------+-----------+
         |                                |
         +---------------+----------------+
                         |
                         v
                +----------------+
                | Chatbot Engine |
                +--------+-------+
                         |
                         v
                  +------------+
                  |  Response  |
                  +------------+
## PROGRAM:
import random
import threading
import time
import re
from collections import Counter

# -----------------------------
# Knowledge Base
# -----------------------------
knowledge_base = {
    "leave": "Employees are entitled to 20 days of annual leave per year.",
    "password": "Password reset requests must be submitted through the IT helpdesk portal.",
    "it support": "IT support can be contacted through the internal helpdesk system.",
    "events": "Annual company events include sports day, cultural fest, and innovation week.",
    "timesheet": "Employees should update their timesheets every Friday.",
    "remote work": "Remote work is allowed with manager approval."
}

# -----------------------------
# Bad Language Filter
# -----------------------------
bad_words = {"stupid", "idiot", "dumb", "badword"}

def filter_bad_language(text):
    words = set(re.findall(r"\w+", text.lower()))
    return not words.isdisjoint(bad_words)

# -----------------------------
# Chatbot Response Function
# -----------------------------
def chatbot_response(user_input):
    text = user_input.lower()

    for key in knowledge_base:
        if key in text:
            return knowledge_base[key]

    return "Sorry, I couldn't find an answer in the organization knowledge base."

# -----------------------------
# Document Processing
# -----------------------------
def process_document(text):

    words = re.findall(r"\w+", text.lower())

    freq = Counter(words)

    common_words = freq.most_common(5)

    summary = " ".join(text.split()[:40])

    print("\nDocument Summary:")
    print(summary)

    print("\nTop Keywords:")
    print(common_words)

# -----------------------------
# OTP Authentication
# -----------------------------
def send_otp():

    otp = random.randint(100000, 999999)

    print("\nOTP sent to your email (simulation):", otp)

    entered = input("Enter OTP: ")

    if str(entered) == str(otp):
        print("Authentication successful\n")
        return True

    print("Invalid OTP")
    return False


# -----------------------------
# Chatbot Session
# -----------------------------
def chatbot_session(user_id):

    print(f"\n--- User {user_id} Connected ---")

    if not send_otp():
        return

    while True:

        user_input = input(f"\nUser{user_id}: ")

        if user_input.lower() == "exit":
            print("Session ended")
            break

        if filter_bad_language(user_input):
            print("Chatbot: Please avoid inappropriate language.")
            continue

        if user_input.startswith("upload"):

            doc = """
            Employees must follow HR policy guidelines.
            HR policy explains leave rules, conduct and attendance.
            Employees should read the HR policy before requesting leave.
            """

            process_document(doc)
            continue

        response = chatbot_response(user_input)

        print("Chatbot:", response)

        time.sleep(1)


# -----------------------------
# Multi User Simulation
# -----------------------------
def start_chatbot():

    users = int(input("Enter number of users (max 5): "))

    threads = []

    for i in range(users):

        t = threading.Thread(target=chatbot_session, args=(i+1,))
        threads.append(t)
        t.start()

    for t in threads:
        t.join()


# -----------------------------
# Main Program
# -----------------------------
if __name__ == "__main__":

    print("\n=== Organization Chatbot ===")
    print("Type 'exit' to quit")
    print("Type 'upload' to test document processing\n")

    start_chatbot()
## OUTPUT:
<img width="1045" height="690" alt="image" src="https://github.com/user-attachments/assets/8262563f-2cc2-4831-b0eb-fca0f651d47a" />

## RESULT:
The chatbot successfully answers organizational queries, authenticates users using OTP, filters inappropriate language, supports multiple users, and summarizes uploaded documents.
