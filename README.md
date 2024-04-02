# Coding-Raja-Task1-
To do list
import json
from datetime import datetime

# Function to load tasks from a JSON file
def load_tasks():
    try:
        with open("tasks.json", "r") as file:
            return json.load(file)
    except FileNotFoundError:
        return []

# Function to save tasks to a JSON file
def save_tasks(tasks):
    with open("tasks.json", "w") as file:
        json.dump(tasks, file, indent=4)

# Function to add a new task
def add_task(tasks, name, priority, due_date):
    tasks.append({
        "name": name,
        "priority": priority,
        "due_date": due_date,
        "completed": False
    })
    save_tasks(tasks)
    print("Task added successfully!")

# Function to remove a task
def remove_task(tasks, task_index):
    del tasks[task_index]
    save_tasks(tasks)
    print("Task removed successfully!")

# Function to mark a task as completed
def complete_task(tasks, task_index):
    tasks[task_index]["completed"] = True
    save_tasks(tasks)
    print("Task marked as completed!")

# Function to display tasks
def display_tasks(tasks):
    if not tasks:
        print("No tasks found.")
    else:
        for index, task in enumerate(tasks):
            status = "Completed" if task["completed"] else "Pending"
            print(f"{index + 1}. {task['name']} - Priority: {task['priority']}, Due Date: {task['due_date']}, Status: {status}")

# Main function
def main():
    tasks = load_tasks()
    while True:
        print("\n*** To-Do List Menu ***")
        print("1. Add Task")
        print("2. Remove Task")
        print("3. Mark Task as Completed")
        print("4. View Tasks")
        print("5. Exit")

        choice = input("Enter your choice: ")

        if choice == "1":
            name = input("Enter task name: ")
            priority = input("Enter priority (High/Medium/Low): ")
            due_date = input("Enter due date (YYYY-MM-DD): ")
            add_task(tasks, name, priority, due_date)
        elif choice == "2":
            display_tasks(tasks)
            task_index = int(input("Enter the index of the task to remove: ")) - 1
            remove_task(tasks, task_index)
        elif choice == "3":
            display_tasks(tasks)
            task_index = int(input("Enter the index of the task to mark as completed: ")) - 1
            complete_task(tasks, task_index)
        elif choice == "4":
            display_tasks(tasks)
        elif choice == "5":
            print("Exiting program. Goodbye!")
            break
        else:
            print("Invalid choice. Please try again.")


