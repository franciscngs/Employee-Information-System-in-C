#include <stdio.h>
#include <string.h>  // Needed for strcspn()

#define CURRENT_YEAR 2025  // Used to compute years in service

// Structure to hold department info
struct Department {
    char deptName[50];
    char position[50];
    int yearHired;
};

// Structure to hold employee info including nested department
struct Employee {
    char employeeID[20];
    char employeeName[50];
    char employeeAddress[100];
    struct Department dept;
};

// Function declarations
void enterRecord();                // Adds a new employee to the file
void displayEmployees();          // Shows all employees' details
void displayLoyaltyAwardees();    // Displays employees with 10+ years of service
int yearsInService(int yearHired); // Calculates years served

int main() {
    int choice;

    while (1) {
        // Main menu display
		// Centered header
		char menuTitle[] = "ABC COMPANY";
		char menuSubtitle[] = "Employees Information System";
		int width = 80;
		
		int padTitle = (width - strlen(menuTitle)) / 2;
		int padSubtitle = (width - strlen(menuSubtitle)) / 2;
		
		printf("\n");
		for (int i = 0; i < padTitle; i++) printf(" ");
		printf("%s\n", menuTitle);
		
		for (int i = 0; i < padSubtitle; i++) printf(" ");
		printf("%s\n\n", menuSubtitle);
        printf("1. Enter new record\n");
        printf("2. Display Employee Information\n");
        printf("3. Display Loyalty Awardees\n");
        printf("4. Exit\n");
        printf("Choice: ");
        scanf("%d", &choice);
        getchar(); // Consumes leftover newline from scanf

        // Menu choices
        if (choice == 1) {
            enterRecord();
        } else if (choice == 2) {
            displayEmployees();
        } else if (choice == 3) {
            displayLoyaltyAwardees();
        } else if (choice == 4) {
            // Exit message
            printf("\nThank you for using this program. Goodbye.\n");
            break;
        } else {
            printf("Invalid choice.\n");
        }
    }

    return 0;
}

// Function to add a new employee record to the file
void enterRecord() {
    struct Employee emp;
    FILE *fp = fopen("record.txt", "a");  // Open file in append mode

    // Get user input for all fields
    printf("\nEmployeeID: ");
    fgets(emp.employeeID, 20, stdin);
    emp.employeeID[strcspn(emp.employeeID, "\n")] = 0;  // Remove newline

    printf("EmployeeName: ");
    fgets(emp.employeeName, 50, stdin);
    emp.employeeName[strcspn(emp.employeeName, "\n")] = 0;

    printf("EmployeeAddress: ");
    fgets(emp.employeeAddress, 100, stdin);
    emp.employeeAddress[strcspn(emp.employeeAddress, "\n")] = 0;

    printf("DeptName: ");
    fgets(emp.dept.deptName, 50, stdin);
    emp.dept.deptName[strcspn(emp.dept.deptName, "\n")] = 0;

    printf("Position: ");
    fgets(emp.dept.position, 50, stdin);
    emp.dept.position[strcspn(emp.dept.position, "\n")] = 0;

    printf("YearHired: ");
    scanf("%d", &emp.dept.yearHired);
    getchar(); // Consume newline

    // Save record in file
    fprintf(fp, "%s|%s|%s|%s|%s|%d\n",
            emp.employeeID, emp.employeeName,
            emp.employeeAddress, emp.dept.deptName,
            emp.dept.position, emp.dept.yearHired);

    fclose(fp);
    printf("Record saved.\n");
}

// Function to display all employee records
void displayEmployees() {
    struct Employee emp;
    FILE *fp = fopen("record.txt", "r");  // Open file in read mode

    if (fp == NULL) {
        printf("No records found.\n");
        return;
    }

    printf("\nEmployee Information:\n");

    // Read each line and display employee info
    while (fscanf(fp, "%[^|]|%[^|]|%[^|]|%[^|]|%[^|]|%d\n",
                  emp.employeeID, emp.employeeName, emp.employeeAddress,
                  emp.dept.deptName, emp.dept.position, &emp.dept.yearHired) == 6) {
        printf("\nEmployeeID: %s\n", emp.employeeID);
        printf("EmployeeName: %s\n", emp.employeeName);
        printf("EmployeeAddress: %s\n", emp.employeeAddress);
        printf("DeptName: %s\n", emp.dept.deptName);
        printf("Position: %s\n", emp.dept.position);
        printf("YearHired: %d\n", emp.dept.yearHired);
    }

    fclose(fp);
}

// Function to display employees eligible for Loyalty Award (10+ years)
void displayLoyaltyAwardees() {
    struct Employee emp;
    FILE *fp = fopen("record.txt", "r");
    int found = 0;

    if (fp == NULL) {
        printf("No records found.\n");
        return;
    }

    // Simulate centered title (assuming 80-character wide console)
    char title1[] = "ABC COMPANY";
    char title2[] = "Loyalty Awardees";
    int width = 80;

    int pad1 = (width - strlen(title1)) / 2;
    int pad2 = (width - strlen(title2)) / 2;

    for (int i = 0; i < pad1; i++) printf(" ");
    printf("%s\n", title1);

    for (int i = 0; i < pad2; i++) printf(" ");
    printf("%s\n\n", title2);

    printf("%-15s %-20s %-25s %s\n", "EmployeeID", "EmployeeName", "Position", "Years in Service");
    printf("-------------------------------------------------------------------------------\n");

    // Read each record, calculate years in service, and display if eligible
    while (fscanf(fp, "%[^|]|%[^|]|%[^|]|%[^|]|%[^|]|%d\n",
                  emp.employeeID, emp.employeeName, emp.employeeAddress,
                  emp.dept.deptName, emp.dept.position, &emp.dept.yearHired) == 6) {
        int years = yearsInService(emp.dept.yearHired);
        if (years >= 10) {
            printf("%-15s %-20s %-25s %d\n",
                   emp.employeeID, emp.employeeName,
                   emp.dept.position, years);
            found = 1;
        }
    }

    if (!found) {
        printf("No employees qualified for Loyalty Award.\n");
    }

    fclose(fp);
}

// Helper function to calculate years in service
int yearsInService(int yearHired) {
    return CURRENT_YEAR - yearHired;
}
