# Tutorial: Running Ollama and Phi3.5 on Raspberry Pi

**Date: June 13, 2025**

## Introduction

Welcome to this step-by-step tutorial! In this guide, you'll learn how to set up Ollama on your Raspberry Pi, install the Phi3.5 language model, test it with a question, and create two Python programs to harness its power. Whether you're an AI enthusiast or just curious about what your Raspberry Pi can do, this tutorial is designed to be approachable and fun. Here's what we'll cover:

- Installing Ollama on your Raspberry Pi
- Adding the Phi3.5 model to Ollama
- Testing Phi3.5 with a terminal question
- Writing a Python program (`ai.py`) to interact with Phi3.5
- Building a blog generator (`ai_blogger.py`) for historic presidents

Let’s dive in and bring some AI magic to your Raspberry Pi!

## Prerequisites

Before we start, make sure you have:

- A Raspberry Pi (Model 4 or higher recommended for better performance)
- Raspberry Pi OS installed and updated
- An internet connection for downloading software and models
- Python 3 (pre-installed on Raspberry Pi OS)
- A terminal and a text editor (like `nano` or `VS Code`)

## Step 1: Install Ollama on Raspberry Pi

First, let’s get Ollama running on your Raspberry Pi.

1. Open a terminal on your Raspberry Pi.
2. Update your system to ensure everything is current:
   ```bash
   sudo apt update
   sudo apt upgrade -y
   sudo apt install python3-requests
   ```
3. Install Ollama by following the official instructions. Visit the Ollama website (typically at `https://ollama.ai`) and look for the Raspberry Pi installation guide. As of now, you might run a command like:
   ```bash
   curl -fsSL https://ollama.ai/install.sh | sh
   ```
   *Note: Check the official site for the exact command, as it may change.*
4. Verify the installation:
   ```bash
   ollama --version
   ```
   If you see a version number, Ollama is ready!

## Step 2: Install Phi3.5 on Ollama

Now, let’s add the Phi3.5 model to Ollama.

1. In the terminal, install Phi3.5 with this command:
   ```bash
   ollama pull phi3.5
   ```
   *Note: This assumes `phi3.5` is the correct model name—confirm it in the Ollama documentation.*
2. Wait for the download to finish. This might take a few minutes depending on your connection and Raspberry Pi model.
3. Check that Phi3.5 is installed:
   ```bash
   ollama list
   ```
   Look for `phi3.5` in the list of models.

## Step 3: Test Phi3.5 in the Terminal

Let’s make sure Phi3.5 works by asking it a question.

1. Start Phi3.5 in an interactive session:
   ```bash
   ollama run phi3.5
   ```
2. Type a simple question, like:
   ```
   What is the tallest mountain in the world?
   ```
3. Press Enter. You should see a response, such as "Mount Everest." If it works, Phi3.5 is up and running!
4. Type `exit` to close the session.

## Step 4: Create `ai.py` with the `LLM(prompt)` Function

Time to write a Python program to talk to Phi3.5 programmatically.
1. Open a text editor and create a file named `ai.py`.
2. Add this code:
   ```python


   def LLM(prompt):
       """
       Sends a prompt to Phi3.5 and returns the response.
       :param prompt: The text to send to Phi3.5
       :return: The response from Phi3.5
       """
       response = requests.post("http://localhost:11434/api/generate", json={"model": "phi3.5", "prompt": prompt, "stream": False})
       result = response.json()
       message = result.get("response", "")
       return message

   # Test the function
   if __name__ == "__main__":
       test_prompt = "What is the tallest mountain in the world?"
       print(LLM(test_prompt))
   ```
   *Note: Adjust the `ollama.generate` call based on the actual API syntax from Ollama’s documentation.*
3. Save the file and run it:
   ```bash
   python ai.py
   ```
   You should see the answer printed in the terminal.

## Step 5: Create `ai_blogger.py` to Generate Blog Posts

Finally, let’s build a program to write blog posts about historic presidents.

1. Create a file named `ai_blogger.py` in the same directory as `ai.py`.
2. Create a folder named `presidents_blog` in the same directory as `ai.py`.
3. Add this code:
   ```python
   from ai import LLM

   # List of historic presidents
   most_historic_presidents = [
       "Abraham Lincoln",
       "George Washington",
       "Franklin D. Roosevelt",
       "Thomas Jefferson",
       "Theodore Roosevelt"
   ]

   # Folder for blog posts
   output_dir = "presidents_blog"


   # Generate blog posts
   for president in most_historic_presidents:
       prompt = f"Write a blog post about {president}"
       blog_post = LLM(prompt)
       filename = f"{president.replace(' ', '_')}.txt"
       with open(f"{output_dir}/{filename}"), "w") as f:
           f.write(blog_post)
       print(f"Saved blog post for {president} to {filename}")
   ```
4. Save the file and run it:
   ```bash
   python ai_blogger.py
   ```
5. Check the `presidents_blog` folder. You’ll find a `.txt` file for each president with their blog post!

## Conclusion

Congratulations! You’ve set up Ollama and Phi3.5 on your Raspberry Pi, tested it, and created two Python programs to interact with it. Your `ai.py` lets you chat with Phi3.5, and `ai_blogger.py` generates blog posts about some of America’s most iconic presidents. Feel free to tweak the prompts or add more presidents to the list!

If you run into any hiccups, check the Ollama documentation or community forums for help. Happy coding, and enjoy your AI-powered Raspberry Pi!

---

*Published on June 13, 2025. Always use the latest software versions for the best experience.*
