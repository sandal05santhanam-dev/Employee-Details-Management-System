# Employee-Details-Management-System
This project is developed using C++ to store and manage employee details. It allows users to enter employee information such as employee ID, name, age, department, and salary. The program helps display employee records in a simple and organized format, making employee information management easy and efficient.
#include <iostream>
#include <string>
#include <iomanip>
using namespace std;

struct Employee
{
    int id;
    string name;
    string department;
    int age;
    float salary;
};

Employee emp[100];
int count = 0;

// Function to add employee details
void addEmployee()
{
    if (count >= 100)
    {
        cout << "\nEmployee storage is full!\n";
        return;
    }

    cout << "\nEnter Employee ID: ";
    cin >> emp[count].id;

    // Check for duplicate ID
    for (int i = 0; i < count; i++)
    {
        if (emp[i].id == emp[count].id)
        {
            cout << "Employee ID already exists!\n";
            return;
        }
    }

    cin.ignore(10000, '\n');

    cout << "Enter Employee Name: ";
    getline(cin, emp[count].name);

    cout << "Enter Department: ";
    getline(cin, emp[count].department);

    cout << "Enter Age: ";
    cin >> emp[count].age;

    cout << "Enter Salary: ";
    cin >> emp[count].salary;

    count++;

    cout << "\nEmployee added successfully!\n";
}

// Function to display all employees
void displayEmployees()
{
    if (count == 0)
    {
        cout << "\nNo employee records available!\n";
        return;
    }

    cout << "\n========== EMPLOYEE DETAILS ==========\n";

    cout << left
         << setw(10) << "ID"
         << setw(22) << "Name"
         << setw(18) << "Department"
         << setw(8) << "Age"
         << setw(12) << "Salary" << endl;

    cout << string(70, '-') << endl;

    for (int i = 0; i < count; i++)
    {
        cout << left
             << setw(10) << emp[i].id
             << setw(22) << emp[i].name
             << setw(18) << emp[i].department
             << setw(8) << emp[i].age
             << fixed << setprecision(2)
             << setw(12) << emp[i].salary << endl;
    }
}

// Function to search for an employee
void searchEmployee()
{
    int id;
    bool found = false;

    cout << "\nEnter Employee ID to search: ";
    cin >> id;

    for (int i = 0; i < count; i++)
    {
        if (emp[i].id == id)
        {
            cout << "\nEmployee Found!\n";
            cout << "Employee ID: " << emp[i].id << endl;
            cout << "Name: " << emp[i].name << endl;
            cout << "Department: " << emp[i].department << endl;
            cout << "Age: " << emp[i].age << endl;
            cout << "Salary: " << emp[i].salary << endl;

            found = true;
            break;
        }
    }

    if (!found)
    {
        cout << "\nEmployee not found!\n";
    }
}

// Function to update employee details
void updateEmployee()
{
    int id;
    bool found = false;

    cout << "\nEnter Employee ID to update: ";
    cin >> id;

    for (int i = 0; i < count; i++)
    {
        if (emp[i].id == id)
        {
            cin.ignore(10000, '\n');

            cout << "Enter New Name: ";
            getline(cin, emp[i].name);

            cout << "Enter New Department: ";
            getline(cin, emp[i].department);

            cout << "Enter New Age: ";
            cin >> emp[i].age;

            cout << "Enter New Salary: ";
            cin >> emp[i].salary;

            cout << "\nEmployee details updated successfully!\n";

            found = true;
            break;
        }
    }

    if (!found)
    {
        cout << "\nEmployee not found!\n";
    }
}

// Function to delete an employee
void deleteEmployee()
{
    int id;
    bool found = false;

    cout << "\nEnter Employee ID to delete: ";
    cin >> id;

    for (int i = 0; i < count; i++)
    {
        if (emp[i].id == id)
        {
            for (int j = i; j < count - 1; j++)
            {
                emp[j] = emp[j + 1];
            }

            count--;

            cout << "\nEmployee deleted successfully!\n";

            found = true;
            break;
        }
    }

    if (!found)
    {
        cout << "\nEmployee not found!\n";
    }
}

// Function to sort employees by salary
void sortEmployees()
{
    if (count == 0)
    {
        cout << "\nNo employee records to sort!\n";
        return;
    }

    for (int i = 0; i < count - 1; i++)
    {
        for (int j = 0; j < count - i - 1; j++)
        {
            if (emp[j].salary > emp[j + 1].salary)
            {
                Employee temp = emp[j];
                emp[j] = emp[j + 1];
                emp[j + 1] = temp;
            }
        }
    }

    cout << "\nEmployees sorted by salary in ascending order!\n";

    displayEmployees();
}

// Main function
int main()
{
    int choice;

    do
    {
        cout << "\n\n====================================\n";
        cout << "     EMPLOYEE MANAGEMENT SYSTEM\n";
        cout << "====================================\n";
        cout << "1. Add Employee\n";
        cout << "2. Display All Employees\n";
        cout << "3. Search Employee\n";
        cout << "4. Update Employee Details\n";
        cout << "5. Delete Employee\n";
        cout << "6. Sort Employees by Salary\n";
        cout << "7. Exit\n";

        cout << "Enter Your Choice: ";
        cin >> choice;

        switch (choice)
        {
            case 1:
                addEmployee();
                break;

            case 2:
                displayEmployees();
                break;

            case 3:
                searchEmployee();
                break;

            case 4:
                updateEmployee();
                break;

            case 5:
                deleteEmployee();
                break;

            case 6:
                sortEmployees();
                break;

            case 7:
                cout << "\nThank you for using the program!\n";
                break;

            default:
                cout << "\nInvalid choice! Please try again.\n";
        }

    } while (choice != 7);

    return 0;
}