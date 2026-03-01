#include <iostream>
#include <fstream>
#include <sstream>
using namespace std;

struct Student {
    string indexNumber;
    string name;
    string program;
};

// Function to register a student
void registerStudent() {
    Student s;
    ofstream file("students.txt", ios::app);

    if (!file) {
        cout << "Error opening file!\n";
        return;
    }

    cout << "\nEnter Index Number: ";
    cin >> s.indexNumber;
    cin.ignore();

    cout << "Enter Name: ";
    getline(cin, s.name);

    cout << "Enter Program: ";
    getline(cin, s.program);

    file << s.indexNumber << "|" << s.name << "|" << s.program << endl;
    file.close();

    cout << "Student registered successfully.\n";
}

// Function to view all students
void viewStudents() {
    ifstream file("students.txt");
    string line;

    if (!file) {
        cout << "No records found.\n";
        return;
    }

    cout << "\n--- Student List ---\n";
    while (getline(file, line)) {
        stringstream ss(line);
        string index, name, program;

        getline(ss, index, '|');
        getline(ss, name, '|');
        getline(ss, program, '|');

        cout << "Index: " << index
             << " | Name: " << name
             << " | Program: " << program << endl;
    }

    file.close();
}

// Function to search student by index
void searchStudent() {
    ifstream file("students.txt");
    string line, searchIndex;
    bool found = false;

    if (!file) {
        cout << "No records found.\n";
        return;
    }

    cout << "\nEnter index number to search: ";
    cin >> searchIndex;

    while (getline(file, line)) {
        stringstream ss(line);
        string index, name, program;

        getline(ss, index, '|');
        getline(ss, name, '|');
        getline(ss, program, '|');

        if (index == searchIndex) {
            cout << "\nStudent Found:\n";
            cout << "Index: " << index << endl;
            cout << "Name: " << name << endl;
            cout << "Program: " << program << endl;
            found = true;
            break;
        }
    }

    if (!found)
        cout << "Student not found.\n";

    file.close();
}

int main() {
    int choice;

    do {
        cout << "\n===== Student Management System =====\n";
        cout << "1. Register Student\n";
        cout << "2. View All Students\n";
        cout << "3. Search Student by Index\n";
        cout << "4. Exit\n";
        cout << "Enter choice: ";
        cin >> choice;

        switch (choice) {
            case 1:
                registerStudent();
                break;
            case 2:
                viewStudents();
                break;
            case 3:
                searchStudent();
                break;
            case 4:
                cout << "Goodbye.\n";
                break;
            default:
                cout << "Invalid choice.\n";
        }

    } while (choice != 4);

    return 0;
} 
