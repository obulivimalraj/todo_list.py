# todo_list.py
# todo_list.py - Simple to-do list manager
import os

def load_tasks(filename="tasks.txt"):
    """Load tasks from file"""
    tasks = []
    if os.path.exists(filename):
        with open(filename, 'r') as file:
            tasks = [line.strip() for line in file if line.strip()]
    return tasks

def save_tasks(tasks, filename="tasks.txt"):
    """Save tasks to file"""
    with open(filename, 'w') as file:
        for task in tasks:
            file.write(task + '\n')

def show_tasks(tasks):
    """Display all tasks"""
    if not tasks:
        print("No tasks in your list!")
    else:
        print("\nYour Tasks:")
        for i, task in enumerate(tasks, 1):
            print(f"{i}. {task}")

def main():
    tasks = load_tasks()
    
    while True:
        print("\n=== Mobile To-Do List ===")
        print("1. View tasks")
        print("2. Add task")
        print("3. Remove task")
        print("4. Exit")
        
        choice = input("Choose option (1-4): ")
        
        if choice == '1':
            show_tasks(tasks)
            
        elif choice == '2':
            task = input("Enter new task: ")
            tasks.append(task)
            save_tasks(tasks)
            print("Task added!")
            
        elif choice == '3':
            show_tasks(tasks)
            if tasks:
                try:
                    task_num = int(input("Enter task number to remove: "))
                    if 1 <= task_num <= len(tasks):
                        removed = tasks.pop(task_num - 1)
                        save_tasks(tasks)
                        print(f"Removed: {removed}")
                    else:
                        print("Invalid task number!")
                except ValueError:
                    print("Please enter a valid number!")
                    
        elif choice == '4':
            print("Goodbye!")
            break
            
        else:
            print("Invalid choice!")

if __name__ == "__main__":
    main()
