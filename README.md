# Data-structure-

#include <iostream>
#include <string>
using namespace std;


struct TaskType 
{
    string task;          // The name or title of the task
    string taskID;        // A unique identifier for the task
    string description;   // A detailed description of the task
    string assigneeID;    // The employee ID of the person assigned to the task
    bool assigned;        // Indicates whether the task is assigned to an employee
};


struct NameType 
{
    string first;
    string middle;
    string last;
};

struct AddressType 
{
    string address;
    string city;
    string region;
};

struct ContactType 
{
    string Phone;
    string Email;
};

struct EmployeeType 
{
    NameType name;
    string age;
    string empID;
    string position;
    string date; // Hire date
    string task;
    string taskID;
    string taskDescription;
    bool assigned;
    AddressType address;
    ContactType contact;
    string deptID; // Department ID
    string salary;
};




struct EmployeeNode 
{
    EmployeeType data;
    EmployeeNode *prev, *next;

    EmployeeNode(EmployeeType new_data) : data(new_data), prev(NULL), next(NULL) {}
};

struct TaskNode 
{
    TaskType data;
    TaskNode *prev, *next;

    TaskNode(TaskType new_data) : data(new_data), prev(NULL), next(NULL) {}
};


bool checkEmployeeExists(EmployeeNode* head, const string& empID) 
{
    EmployeeNode* current = head;
    while (current != NULL) 
	{
        if (current->data.empID == empID) 
		{
            return true;  // Employee ID found in the list
        }
        current = current->next;
    }
    return false;  // Employee ID not found
}

void getUniqueEmployeeID(EmployeeNode* head, string& empID)
{
    bool found;
    do {
        found = false;
        cout << "Employee ID: ";
        cin >> empID;

        if (checkEmployeeExists(head, empID)) 
		{
            found = true;
            cout << "Employee ID already exists.\n";
        }
    } while (found);
}



void getEmployeeDetails(EmployeeNode* head, EmployeeType &employee) 
{
    cout << "Enter first name: ";
    cin >> employee.name.first;
    cout << "Enter middle name: ";
    cin >> employee.name.middle;
    cout << "Enter last name: ";
    cin >> employee.name.last;
	cout << "Enter age: ";
    cin >> employee.age;
	getUniqueEmployeeID(head, employee.empID); 
    cout << "Enter position: ";
    cin >> employee.position;
    cout << "Enter employee hire date: ";
    cin >> employee.date;
    cout << "Enter task: ";
    cin >> employee.task;
    cout << "Enter task ID: ";
    cin >> employee.taskID;
	cout << "Enter task Description: ";
    cin >> employee.taskDescription;
    cout << "Enter address: ";
    cin >> employee.address.address;
    cout << "Enter city: ";
    cin >> employee.address.city;
    cout << "Enter region: ";
    cin >> employee.address.region;
    cout << "Enter Email: ";
    cin >> employee.contact.Email;
    cout << "Enter Phone: ";
    cin >> employee.contact.Phone;
    cout << "Enter dept ID: ";
    cin >> employee.deptID;
    cout << "Enter salary: ";
    cin >> employee.salary;
    cout << "employee added succsesfully. \n\n";
}

void updateEmployee(EmployeeNode* head, EmployeeType &employee) 
{
	if(head == NULL)
	{
		cout << "\nSystem is empty. \n";
		return;
	}
	
    string empID;
    cout << "\nEnter employee ID to update data: ";
    cin >> empID;

    EmployeeNode* current = head;
    while (current != NULL && current->data.empID != empID) 
	{
        current = current->next;
    }

    if (current == NULL) 
	{
        cout << "\nEmployee was not found.\n\n";
        return;
    }

	cout << "Enter first name: ";
    cin >> current->data.name.first;
    cout << "Enter middle name: ";
    cin >> current->data.name.middle;
    cout << "Enter last name: ";
    cin >> current->data.name.last;
	cout << "Enter age: ";
    cin >> current->data.age;
    
    bool found;
    do {
        found = false;
        string ID;
        cout << "Employee ID: ";
        cin >> ID;

        if (checkEmployeeExists(head, ID)) 
		{
            found = true;
            cout << "Employee ID already exists.\n";
        }
        else
        {
        	current->data.empID = ID;
		}
    } while (found);    
    
	cout << "Enter position: ";
    cin >> current->data.position;
    cout << "Enter employee hire date: ";
    cin >> current->data.date;
    cout << "Enter task: ";
    cin >> current->data.task;
    cout << "Enter task ID: ";
    cin >> current->data.taskID;
	cout << "Enter task Description: ";
    cin >> current->data.taskDescription;
    cout << "Enter address: ";
    cin >> current->data.address.address;
    cout << "Enter city: ";
    cin >> current->data.address.city;
    cout << "Enter region: ";
    cin >> current->data.address.region;
    cout << "Enter Email: ";
    cin >> current->data.contact.Email;
    cout << "Enter Phone: ";
    cin >> current->data.contact.Phone;
    cout << "Enter dept ID: ";
    cin >> current->data.deptID;
    cout << "Enter salary: ";
    cin >> current->data.salary;
    cout << "Employee data updated successfully.\n";
}


void getTaskDetails(TaskType &task) 
{
    cout << "Enter task title: ";
    cin >> task.task;  // Input for task title

    cout << "Enter task ID: ";
    cin >> task.taskID;  // Input for task ID

    cout << "Enter task description: ";
    cin.ignore();  // Ignore leftover newline character from previous input
    getline(cin, task.description);  // Input for task description

    cout << "Enter assignee ID (leave empty if not assigned): ";
    getline(cin, task.assigneeID);
    
    cout << "Is the task assigned? (1 for yes, 0 for no): ";
    cin >> task.assigned;  // Input for whether the task is assigned
}


void updateTask(TaskNode* head) 
{
    if (head == NULL) 
	{
        cout << "\nThe task list is empty.\n\n";
        return;
    }

    string taskID;
    cout << "\nEnter the task ID to update: ";
    cin >> taskID;

    TaskNode* current = head;
    while (current != NULL && current->data.taskID != taskID) 
	{
        current = current->next;
    }

    if (current != NULL) 
	{
		
    	cout << "Update task title [" << current->data.task << "]: ";
    	cin >> current->data.task;  // Update task title

    	cout << "Update task description: ";
    	cin.ignore();  // Ignore leftover newline character from previous input
    	getline(cin, current->data.description);  // Update task description

    	cout << "Update assignee ID (leave empty if not): [" << current->data.assigneeID << "]: ";
    	cin >> current->data.assigneeID;  // Update assignee ID

    	cout << "Is the task assigned? (1 for yes, 0 for no): [" << current->data.assigned << "]: ";
    	cin >> current->data.assigned;  // Update whether the task is assigned

        cout << "Task updated successfully.\n";
    } 
	else 
	{
        cout << "\nTask with ID " << taskID << " not found.\n\n";
    }
}



void deleteEmployee(EmployeeNode* &head, string empID, TaskNode* taskRoot) 
{
    if (head == NULL) 
	{
        cout << "\nthe system is empty.\n\n";
        return;
    }

    cout << "\nenter the employee's ID to delete: \n";
    cin >> empID;

    EmployeeNode* current = head;
    while (current != NULL && current->data.empID != empID) 
	{
        current = current->next;
    }

    if (current == NULL) 
	{
        cout << "\nemployee was not found.\n\n";
        return; // Employee not found
    }

    // Check if the employee is assigned to any task
    if (current->data.assigned) 
	{
        TaskNode* taskCurrent = taskRoot;
        while (taskCurrent != NULL) 
		{
            if (taskCurrent->data.assigneeID == empID) 
			{
                // Clear assignee information from the task record
                taskCurrent->data.assigneeID = "";
                taskCurrent->data.assigned = false;
                break;
            }
            taskCurrent = taskCurrent->next;
        }
    }

    // Delete the employee
    if (current->prev != NULL) 
	{
        current->prev->next = current->next;
    } else 
	{
        head = current->next;  // Update head if the first node is being deleted
    }

    if (current->next != NULL) 
	{
        current->next->prev = current->prev;
    }

    delete current;  // Free the memory of the node
    cout << "\nemployee was deleted successfully. \n\n";
}



void deleteTask(TaskNode* &head, string taskID, EmployeeNode* employeeRoot) 
{
    if (head == NULL) 
	{
        cout << "\nThe task list is empty.\n\n";
        return;
    }

    cout << "\nEnter the task ID to delete: ";
    cin >> taskID;

    TaskNode* current = head;
    while (current != NULL && current->data.taskID != taskID) 
	{
        current = current->next;
    }

    if (current == NULL) 
	{
        cout << "\nTask with ID " << taskID << " was not found.\n\n";
        return; // Task not found
    }
    // Check if the task is assigned to any employee
    if (current->data.assigned) 
	{
        EmployeeNode* employeeCurrent = employeeRoot;
        while (employeeCurrent != NULL) 
		{
            if (employeeCurrent->data.taskID == taskID) 
			{
                // Clear task information from the employee record
                employeeCurrent->data.task = "";
                employeeCurrent->data.taskID = "";
                employeeCurrent->data.taskDescription = "";
                employeeCurrent->data.assigned = false;
                break;
            }
            employeeCurrent = employeeCurrent->next;
        }
    }
    // Delete the task
    if (current->prev != NULL) 
	{
        current->prev->next = current->next;
    } else {
        head = current->next;  // Update head if the first node is being deleted
    }

    if (current->next != NULL) 
	{
        current->next->prev = current->prev;
    }

    delete current;  // Free the memory of the node
    cout << "\nTask was deleted successfully.\n\n";
}



void insertEmployee(EmployeeNode* &head, EmployeeType data) 
{
    EmployeeNode* newNode = new EmployeeNode(data);
    if (head == NULL) 
	{
        head = newNode;
        return;
    }

    EmployeeNode* current = head;
    while (current->next != NULL) 
	{
        current = current->next;
    }

    current->next = newNode;
    newNode->prev = current;
}

void insertTask(TaskNode* &head, TaskType data) 
{
    TaskNode* newNode = new TaskNode(data);
    if (head == NULL) 
	{
        head = newNode;
        return;
    }

    TaskNode* current = head;
    while (current->next != NULL) 
	{
        current = current->next;
    }

    current->next = newNode;
    newNode->prev = current;
}


EmployeeNode* searchEmployee(EmployeeNode* head, string empID) 
{
    EmployeeNode* current = head;
    while (current != NULL) 
	{
        if (current->data.empID == empID) 
		{
            return current;
        }
        current = current->next;
    }
    return NULL; // Employee not found
}

TaskNode* searchTask(TaskNode* head, string taskID) 
{
    TaskNode* current = head;
    while (current != NULL) 
	{
        if (current->data.taskID == taskID) 
		{
            return current;
        }
        current = current->next;
    }
    cout <<"\ntask was not found.\n";
    return NULL; // Task not found
}

void assignTaskToEmployee(EmployeeNode* employeeRoot, TaskNode* taskRoot) 
{
    if (employeeRoot == NULL) 
	{
        cout << "\nNo employees available.\n";
        return;
    }

    if (taskRoot == NULL) 
	{
        cout << "\nNo tasks available.\n";
        return;
    }

    string empID, taskID;
    cout << "Enter Employee ID: ";
    cin >> empID;

    EmployeeNode* employee = searchEmployee(employeeRoot, empID);
    if (employee == NULL) 
	{
        cout << "Employee not found.\n";
        return;
    }

    cout << "Enter Task ID: ";
    cin >> taskID;

    TaskNode* task = searchTask(taskRoot, taskID);
    if (task == NULL) 
	{
        cout << "Task not found.\n";
        return;
    }

    if (task->data.assigned) 
	{
        cout << "This task is already assigned.\n";
        return;
    }

    // Assign task details to employee and mark the task as assigned
    employee->data.task = task->data.task;
    employee->data.taskID = task->data.taskID;
    employee->data.taskDescription = task->data.description;
    employee->data.assigned = true;

    task->data.assigneeID = empID;
    task->data.assigned = true;

    cout << "Task assigned successfully.\n";
}



void inOrderEmployee(EmployeeNode* head) 
{
    EmployeeNode* current = head;
    int i = 1;
    if(current != NULL)
    {
    	while (current != NULL) 
		{
       		cout << "\nEmployee number " << i << " data: \n";
        	cout << "Name: " << current->data.name.first << " " << current->data.name.middle << " " << current->data.name.last << endl;
			cout << "Age: " << current->data.age;
    		cout << "\nID: " << current->data.empID;
    		cout << "\nposition: " << current->data.position;
    		cout << "\nhire date: " <<  current->data.date;
    		cout << "\ntask: " << current->data.task;
    		cout << "\ntask ID: "<< current->data.taskID;
			cout << "\ntask Description: " << current->data.taskDescription ;
    		cout << "\naddress: " << current->data.address.address;
    		cout << "\ncity: " << current->data.address.city;
    		cout << "\nregion: " << current->data.address.region ;
    		cout << "\nEmail: " << current->data.contact.Email;
    		cout << "\nPhone: "<< current->data.contact.Phone;
    		cout << "\ndept ID: "<< current->data.deptID;
    		cout << "\nsalary: "<< current->data.salary << "\n\n";
			current = current->next;
        	i++;
    	}
    }
    else 
    {
    	cout << "\nthe system is empty.\n\n";
	}
}

void EmployeeINFO(EmployeeNode* foundEmployee) 
{
		
		if(foundEmployee != NULL)
		{
			cout << "\nTHE EMPLOYEE INFORMATIONS: \n";
        	cout << "Name: " << foundEmployee->data.name.first << " " << foundEmployee->data.name.middle << " " << foundEmployee->data.name.last << endl;
			cout << "Age: " << foundEmployee->data.age;
    		cout << "\nID: " << foundEmployee->data.empID;
    		cout << "\nposition: " << foundEmployee->data.position;
    		cout << "\nhire date: " <<  foundEmployee->data.date;
    		cout << "\ntask: " << foundEmployee->data.task;
    		cout << "\ntask ID: "<< foundEmployee->data.taskID;
			cout << "\ntask Description: " << foundEmployee->data.taskDescription ;
    		cout << "\naddress: " << foundEmployee->data.address.address;
    		cout << "\ncity: " << foundEmployee->data.address.city;
    		cout << "\nregion: " << foundEmployee->data.address.region ;
    		cout << "\nEmail: " << foundEmployee->data.contact.Email;
    		cout << "\nPhone: "<< foundEmployee->data.contact.Phone;
    		cout << "\ndept ID: "<< foundEmployee->data.deptID;
    		cout << "\nsalary: "<< foundEmployee->data.salary << "\n\n" ;
        }

    
}



void EmployeeINFOshort(EmployeeNode* head) 
{
    EmployeeNode* current = head;
    if(current != NULL)
    {
    	while (current != NULL) 
		{
       		cout << "\nAll Employees Data: \n";
        	cout << "Name: " << current->data.name.first << " " << current->data.name.middle << " " << current->data.name.last << endl;
    		cout << "ID: " << current->data.empID << endl;
			current = current->next;
    	}
    }
    else 
    {
    	cout << "\nthe system is empty.\n\n";
	}
}


void inOrderTask(TaskNode* head) 
{
    TaskNode* current = head;
    if(current != NULL)
    {
    	while (current != NULL) 
		{
			cout << "Task title: " << current->data.task << endl;
        	cout << "Task ID: " << current->data.taskID << endl;
			cout << "Task description: " << current->data.description << endl;
			cout << "Task assigned to employee: " << current->data.assigneeID << "\n\n";
			
        	current = current->next;
    	}
    }
    else
    {
    	cout << "\nNO tasks available.\n\n";
	}
}


int main() 
{
	EmployeeNode* employeeRoot = NULL;
	TaskNode* taskRoot = NULL;

    int choice;
    EmployeeType newEmployee;
    TaskType newTask;
    string curID, taskID;

    do {
        // Display menu and get user choice
        cout << "\n\n---------WELCOME TO THE EMPLOYEE MANGAEMENT SYSTEM---------\n";
		cout << "1. Add Employee.\n";
        cout << "2. Add Task.\n";
        cout << "3. Assign Task to Employee.\n";
        cout << "4. Display all employees.\n";
        cout << "5. Display All Tasks.\n";
        cout << "6. Search Employee.\n";
        cout << "7. Update Employee.\n";
        cout << "8. Update Task.\n";
        cout << "9. Delete Employee.\n";
        cout << "10. Delete Task.\n";
        cout << "11. EXIT FROM THE SYSTEM\n";
        cout << "-----------------------------------------------------------\n";
        cout << "Enter your choice: ";
        
        cin >> choice;
        switch (choice) 
		{
            case 1: // Add Employee
            {
			    getEmployeeDetails(employeeRoot, newEmployee);
                insertEmployee(employeeRoot, newEmployee);
                break;
    		}
			case 2: // Add Task
            {    getTaskDetails(newTask);
                 insertTask(taskRoot, newTask);
                break;
        	}
			case 3: // Assign Task to Employee
            {   assignTaskToEmployee(employeeRoot, taskRoot);
                break;
            }
            case 4: // Display All Employees
            {
                inOrderEmployee(employeeRoot);
                break;
            }
            case 5: // Display All Tasks 
            {
                inOrderTask(taskRoot);
                break;
            }
			case 6: // Search Employee
			{    
				EmployeeINFOshort(employeeRoot);
    			cout << "\nEnter the employee's ID to search: ";
    			cin >> curID;
    			EmployeeNode* foundEmployee = searchEmployee(employeeRoot, curID);
    			if (foundEmployee != NULL) 
				{
     		    	EmployeeINFO(foundEmployee);
    			} 
				else 
				{
        			cout << "Employee with ID " << curID << " not found.\n";
    			}
    			break;
			}
            case 7: // Update Employee
            {	
            	EmployeeINFOshort(employeeRoot);
            	updateEmployee(employeeRoot, newEmployee);
				break;
            }
			case 8: // Update Task
            {    
				updateTask(taskRoot);
                break;
            }
            case 9: // Delete Employee
            {	
                deleteEmployee(employeeRoot, curID, taskRoot);
                break;
            }
            case 10: // Delete Task
            {
                deleteTask(taskRoot, taskID, employeeRoot);
                break; 
            }
			case 11: // Exit
            {
                cout << "Exiting Employee Management System.\n";
                break;
            }
			default:
                cout << "Invalid choice. Please try again.\n";
        }
    } while (choice != 11);

    return 0;
}
