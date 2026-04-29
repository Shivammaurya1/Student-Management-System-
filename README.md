# Student-Management-System-
#include <iostream>
#include <string>
using namespace std;

const int MAX_STUDENTS = 100;

struct Student {
    int rollNo;
    string name;
    float marks;
};

Student students[MAX_STUDENTS];
int studentCount = 0;

void addStudents(int n) {
    if (n > MAX_STUDENTS) {
        cout << "Error: Max limit is " << MAX_STUDENTS << endl;
        return;
    }

    for (int i = 0; i < n; i++) {
        Student s;
        cout << "\n--- Student " << (i + 1) << " ---\n";

        cout << "Enter Roll No: ";
        cin >> s.rollNo;

        bool duplicate = false;
        for (int j = 0; j < studentCount; j++) {
            if (students[j].rollNo == s.rollNo) {
                cout << "Duplicate Roll Number! Skipping...\n";
                duplicate = true;
                break;
            }
        }
        if (duplicate) continue;

        cout << "Enter Name: ";
        cin.ignore();
        getline(cin, s.name);

        do {
            cout << "Enter Marks (0-100): ";
            cin >> s.marks;
        } while (s.marks < 0 || s.marks > 100);

        students[studentCount++] = s;
        cout << "Added Successfully!\n";
    }
}

void searchStudent() {
    int roll;
    cout << "\nEnter Roll No to Search: ";
    cin >> roll;

    for (int i = 0; i < studentCount; i++) {
        if (students[i].rollNo == roll) {
            cout << "\nFound!\n";
            cout << "Name: " << students[i].name << endl;
            cout << "Marks: " << students[i].marks << endl;
            return;
        }
    }
    cout << "Student Not Found!\n";
}

int main() {
    int n;
    cout << "How many students? ";
    cin >> n;

    addStudents(n);
    searchStudent();

    return 0;
}
