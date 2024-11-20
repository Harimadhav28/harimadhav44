import streamlit as st
import random

# Set a title
st.title("Number Guessing Game")

# Initialize the secret number and attempts (store these values in session state)
if 'secret_number' not in st.session_state:
    st.session_state.secret_number = random.randint(1, 100)
if 'attempts' not in st.session_state:
    st.session_state.attempts = 0

# Input for user's guess
st.write("Guess the secret number between 1 and 100:")
user_guess = st.number_input("Enter your guess:", min_value=1, max_value=100, step=1)

# Button to submit the guess
if st.button("Check Guess"):
    st.session_state.attempts += 1
    if user_guess == st.session_state.secret_number:
        st.success(f"Congratulations! You guessed it in {st.session_state.attempts} attempts ")
        st.session_state.secret_number = random.randint(1, 100)  # Reset for a new game
        st.session_state.attempts = 0
    elif user_guess < st.session_state.secret_number:
        st.info("Try a higher number!")
    else:
        st.info("Try a lower number!")

# Display the number of attempts
st.write(f"Attempts: {st.session_state.attempts}")
