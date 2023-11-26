# lab-8
import requests
import json
import random

# Task 1
# 1.1 GET Request
post_id = 1
response = requests.get(f"https://jsonplaceholder.typicode.com/todos/{post_id}")
if response.status_code >= 400:
    print(f"Error: {response.status_code}")
else:
    print("GET Request Content:", response.json())

# 1.2 Create ToDo class
class ToDo:
    def __init__(self, userId, id, title, completed):
        self.userId = userId
        self.id = id
        self.title = title
        self.completed = completed

# 1.3 Create new object
new_todo = ToDo(1, 1, "New ToDo", False)

# 1.4 POST Request
new_todo_dict = {
    "userId": new_todo.userId,
    "id": new_todo.id,
    "title": new_todo.title,
    "completed": new_todo.completed
}
response_post = requests.post("https://jsonplaceholder.typicode.com/todos", json=new_todo_dict)
if response_post.status_code >= 400:
    print(f"Error: {response_post.status_code}")
else:
    print("POST Request Content:", response_post.json())

# 1.5 Edit data
new_todo.completed = True

# 1.6 PUT Request
updated_todo_dict = {
    "userId": new_todo.userId,
    "id": new_todo.id,
    "title": new_todo.title,
    "completed": new_todo.completed
}
chosen_id = 1  # Replace with the chosen todo item ID
response_put = requests.put(f"https://jsonplaceholder.typicode.com/todos/{chosen_id}", json=updated_todo_dict)
if response_put.status_code >= 400:
    print(f"Error: {response_put.status_code}")
else:
    print("PUT Request Content:", response_put.json())

# Task 2
# 2.1 Random Character Request
character_id = random.randint(1, 826)
character_response = requests.get(f"https://rickandmortyapi.com/api/character/{character_id}")
print("2.2 Response:", character_response.json())
print("2.2 Keys:", character_response.json().keys())

# 2.3 Save to File
with open(f"info_character_{character_id}.json", 'w') as file:
    json.dump(character_response.json(), file)

# 2.4 Episode List
episodes = character_response.json()['episode']
episode_ids = [episode.split('/')[-1] for episode in episodes]

with open(f"all_episodes_with_character_{character_id}", 'a') as file:
    for episode_id in episode_ids:
        file.write(f"https://rickandmortyapi.com/api/episode/{episode_id}\n")

# 2.5 Episode Response Structure
episode_response = requests.get("https://rickandmortyapi.com/api/episode/1")
print("2.5 Episode Response:", episode_response.json())

# 2.6 Episode Class Creation (Episode.py)
# Define Episode class with attributes obtained from episode response

# 2.7 Episode Data Retrieval
# Iterate through episode ids, make requests, create Episode objects, and store them in a list

# 2.8 Class Methods
# Add methods to the Episode class

# 2.9 Character Response Structure
character_response = requests.get("https://rickandmortyapi.com/api/character/1")
print("2.9 Character Response:", character_response.json())

# 2.10 Character Class Creation (Character.py)
# Define Character class with attributes obtained from character response

# 2.11 Character Object Creation
# Create an object "random_character" of the "Character" class

# 2.12 Character Class Methods
# Add methods to the Character class

# 2.13 Results
# Show all results
