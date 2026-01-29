# python-todo-app
# Simple Python to-do list application for managing tasks via command line. #
import json

tasks = []

def load_tasks():
    global tasks
    try:
        with open("tasks.json", "r") as f:
            tasks = json.load(f)
    except:
        tasks = []

def save_tasks():
    with open("tasks.json", "w") as f:
        json.dump(tasks, f, indent=4)

def add_task():
    task = input("Anna tehtävä: ")
    tasks.append({"task": task, "done": False})
    save_tasks()
    print("Tehtävä lisätty!")

def show_tasks():
    if not tasks:
        print("Ei tehtäviä.")
        return
    for i, t in enumerate(tasks):
        status = "✔" if t["done"] else "❌"
        print(f"{i+1}. {t['task']} [{status}]")

def mark_done():
    show_tasks()
    num = int(input("Valitse tehtävä numero: "))
    tasks[num-1]["done"] = True
    save_tasks()
    print("Merkitty tehdyksi!")

def delete_task():
    show_tasks()
    num = int(input("Poista tehtävä numero: "))
    tasks.pop(num-1)
    save_tasks()
    print("Tehtävä poistettu!")

def main():
    load_tasks()
    while True:
        print("\n1. Lisää tehtävä")
        print("2. Näytä tehtävät")
        print("3. Merkitse tehdyksi")
        print("4. Poista tehtävä")
        print("5. Lopeta")

        choice = input("Valinta: ")

        if choice == "1":
            add_task()
        elif choice == "2":
            show_tasks()
        elif choice == "3":
            mark_done()
        elif choice == "4":
            delete_task()
        elif choice == "5":
            print("Moi!")
            break
        else:
            print("Virheellinen valinta!")

main()

