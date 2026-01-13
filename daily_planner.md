# Daily Planner Skill

This skill helps you plan and organize your daily schedule efficiently.

## Description
An interactive tool that allows you to add tasks for the day, set priorities, and view an organized schedule. The planner helps you prioritize and allocate time effectively by letting you input tasks, assign priority levels, estimate time requirements, and visualize your daily schedule.

## Usage
```
/daily-planner
```

## Implementation
```python
#!/usr/bin/env python3

import datetime

class DailyPlanner:
    def __init__(self):
        self.tasks = []

    def add_task(self):
        print("\n--- Add New Task ---")
        task_name = input("Enter task name: ").strip()

        if not task_name:
            print("Task name cannot be empty!")
            return

        print("Select priority level:")
        print("1. High")
        print("2. Medium")
        print("3. Low")

        priority_choice = input("Enter priority (1-3): ").strip()
        priority_map = {"1": "High", "2": "Medium", "3": "Low"}
        priority = priority_map.get(priority_choice, "Medium")

        estimated_time = input("Estimated time required (e.g., 30 mins, 1 hour): ").strip()

        task = {
            "name": task_name,
            "priority": priority,
            "estimated_time": estimated_time,
            "completed": False
        }

        self.tasks.append(task)
        print(f"Task '{task_name}' added successfully!")

    def view_schedule(self):
        if not self.tasks:
            print("\nNo tasks added yet. Add some tasks first!")
            return

        print("\n--- Today's Schedule ---")
        print(f"Date: {datetime.date.today().strftime('%A, %B %d, %Y')}")
        print("-" * 50)

        # Sort tasks by priority (High first, then Medium, then Low)
        priority_order = {"High": 1, "Medium": 2, "Low": 3}
        sorted_tasks = sorted(self.tasks, key=lambda x: priority_order[x["priority"]])

        for i, task in enumerate(sorted_tasks, 1):
            status = "✓" if task["completed"] else "○"
            print(f"{i}. [{status}] {task['name']}")
            print(f"   Priority: {task['priority']}")
            print(f"   Estimated Time: {task['estimated_time']}")
            print()

    def mark_completed(self):
        if not self.tasks:
            print("\nNo tasks added yet. Add some tasks first!")
            return

        print("\n--- Mark Task as Completed ---")
        self.view_schedule()

        try:
            task_num = int(input("Enter task number to mark as completed (0 to cancel): "))

            if task_num == 0:
                return

            if 1 <= task_num <= len(self.tasks):
                task_index = task_num - 1
                # Since we sort when displaying, we need to map back
                priority_order = {"High": 1, "Medium": 2, "Low"}
                sorted_tasks = sorted(self.tasks, key=lambda x: priority_order[x["priority"]])

                original_index = self.tasks.index(sorted_tasks[task_index])
                self.tasks[original_index]["completed"] = True

                print(f"Task '{sorted_tasks[task_index]['name']}' marked as completed!")
            else:
                print("Invalid task number!")
        except ValueError:
            print("Please enter a valid number!")

    def remove_task(self):
        if not self.tasks:
            print("\nNo tasks to remove.")
            return

        print("\n--- Remove Task ---")
        self.view_schedule()

        try:
            task_num = int(input("Enter task number to remove (0 to cancel): "))

            if task_num == 0:
                return

            if 1 <= task_num <= len(self.tasks):
                # Since we sort when displaying, we need to map back
                priority_order = {"High": 1, "Medium": 2, "Low"}
                sorted_tasks = sorted(self.tasks, key=lambda x: priority_order[x["priority"]])

                task_to_remove = sorted_tasks[task_num - 1]
                self.tasks.remove(task_to_remove)

                print(f"Task '{task_to_remove['name']}' removed successfully!")
            else:
                print("Invalid task number!")
        except ValueError:
            print("Please enter a valid number!")

    def show_menu(self):
        print("\n" + "="*50)
        print("           DAILY PLANNER")
        print("="*50)
        print("1. Add a new task")
        print("2. View today's schedule")
        print("3. Mark task as completed")
        print("4. Remove a task")
        print("5. Exit")
        print("-"*50)

    def run(self):
        print("Welcome to Daily Planner!")
        print("Plan your day effectively by adding tasks and setting priorities.")

        while True:
            self.show_menu()
            choice = input("Select an option (1-5): ").strip()

            if choice == "1":
                self.add_task()
            elif choice == "2":
                self.view_schedule()
            elif choice == "3":
                self.mark_completed()
            elif choice == "4":
                self.remove_task()
            elif choice == "5":
                print("\nGoodbye! Have a productive day!")
                break
            else:
                print("\nInvalid choice. Please select 1-5.")

            if choice in ["1", "3", "4"]:
                input("\nPress Enter to continue...")

def main():
    planner = DailyPlanner()
    planner.run()

if __name__ == "__main__":
    main()
```

## Tags
- productivity
- planning
- schedule
- organization
- task-management