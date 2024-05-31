# To-do-list-in-c
#include <iostream>
#include <vector>
#include <string>

using namespace std;

class Task {
public:
    string description;
    bool completed;

    Task(string desc) : description(desc), completed(false) {}
};

class ToDoList {
private:
    vector<Task> tasks;

public:
    void addTask(const string &task) {
        tasks.emplace_back(task);
    }

    void completeTask(int index) {
        if (index >= 0 && index < tasks.size()) {
            tasks[index].completed = true;
        } else {
            cout << "Invalid task number" << endl;
        }
    }

    void viewTasks() const {
        for (size_t i = 0; i < tasks.size(); ++i) {
            cout << i + 1 << ". " << tasks[i].description
                 << " - " << (tasks[i].completed ? "Completed" : "Not Completed") << endl;
        }
    }
};

void displayMenu() {
    cout << "\nTo-Do List Application" << endl;
    cout << "1. Add a task" << endl;
    cout << "2. Mark a task as completed" << endl;
    cout << "3. View tasks" << endl;
    cout << "4. Exit" << endl;
}

int main() {
    ToDoList todoList;
    int choice;

    while (true) {
        displayMenu();
        cout << "Choose an option: ";
        cin >> choice;
        cin.ignore(); // Ignore the newline character left in the buffer

        if (choice == 1) {
            string task;
            cout << "Enter the task: ";
            getline(cin, task);
            todoList.addTask(task);
            cout << "Task added." << endl;
        } else if (choice == 2) {
            todoList.viewTasks();
            int taskNum;
            cout << "Enter the number of the task to mark as completed: ";
            cin >> taskNum;
            cin.ignore(); // Ignore the newline character left in the buffer
            todoList.completeTask(taskNum - 1);
            cout << "Task marked as completed." << endl;
        } else if (choice == 3) {
            todoList.viewTasks();
        } else if (choice == 4) {
            cout << "Exiting the application." << endl;
            break;
        } else {
            cout << "Invalid choice. Please try again." << endl;
        }
    }

    return 0;
}
