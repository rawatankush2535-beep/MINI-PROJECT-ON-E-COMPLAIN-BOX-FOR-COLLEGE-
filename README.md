#include <iostream> 
#include <vector> 
#include <fstream> 
using namespace std; 
struct Complaint { 
    string name; 
    string enrollment; 
    string department; 
    string category; 
    string problem; 
    string status; 
}; 
void showMenu() { 
    cout << "\n========== COLLEGE E-COMPLAINT BOX ==========\n"; 
    cout << "1. Submit Complaint\n"; 
    cout << "2. View All Complaints\n"; 
    cout << "3. Search by Enrollment Number\n"; 
    cout << "4. Exit\n"; 
    cout << "Enter your choice: "; 
} 
void submitComplaint(vector<Complaint> &complaints) { 
 
    Complaint c; 
    cin.ignore(); 
 
    cout << "\nEnter Student Name: "; 
    getline(cin, c.name); 
 
    cout << "Enter Enrollment Number: "; 
    getline(cin, c.enrollment); 
 
 
 
 
    cout << "Enter Department: "; 
    getline(cin, c.department); 
 
    cout << "\nSelect Complaint Category\n"; 
    cout << "1. Academic Problem\n"; 
    cout << "2. Infrastructure Issue\n"; 
    cout << "3. Faculty Issue\n"; 
    cout << "4. Library Issue\n"; 
    cout << "5. Department Issue\n"; 
    cout << "6. Other\n"; 
    cout << "Enter choice: "; 
 
    int catChoice; 
    cin >> catChoice; 
    cin.ignore(); 
 
    switch(catChoice) { 
        case 1: c.category = "Academic Problem"; break; 
        case 2: c.category = "Infrastructure Issue"; break; 
        case 3: c.category = "Faculty Issue"; break; 
        case 4: c.category = "Library Issue"; break; 
        case 5: c.category = "Department Issue"; break; 
        case 6: c.category = "Other"; break; 
        default: c.category = "Unknown"; break; 
    } 
 
    cout << "\nEnter Your Problem: "; 
    getline(cin, c.problem); 
 
    c.status = "Pending"; 
    complaints.push_back(c); 
    ofstream file("complaints.txt", ios::app); 
    file << c.name << "|" 
         << c.enrollment << "|" 
 
 
 
         << c.department << "|" 
         << c.category << "|" 
         << c.problem << "|" 
         << c.status << endl; 
    file.close(); 
 
    cout << "\nComplaint Submitted Successfully!\n"; 
} 
void viewComplaints(vector<Complaint> &complaints) { 
 
    if(complaints.empty()) { 
        cout << "\nNo complaints available.\n"; 
        return; 
    } 
 
    cout << "\n=========== ALL COMPLAINTS ===========\n"; 
 
    for(int i=0;i<complaints.size();i++) { 
 
        cout << "\nComplaint ID: " << i+1 << endl; 
        cout << "Name: " << complaints[i].name << endl; 
        cout << "Enrollment: " << complaints[i].enrollment << endl; 
        cout << "Department: " << complaints[i].department << endl; 
        cout << "Category: " << complaints[i].category << endl; 
        cout << "Problem: " << complaints[i].problem << endl; 
        cout << "Status: " << complaints[i].status << endl; 
        cout << "---------------------------------\n"; 
    } 
} 
void searchComplaint(vector<Complaint> &complaints) { 
 
    string enroll; 
    cout << "\nEnter Enrollment Number: "; 
    cin >> enroll; 
 
 
 
 
    bool found=false; 
 
    for(int i=0;i<complaints.size();i++) { 
 
        if(complaints[i].enrollment==enroll) { 
 
            cout << "\nComplaint Found\n"; 
            cout << "Name: " << complaints[i].name << endl; 
            cout << "Department: " << complaints[i].department << endl; 
            cout << "Category: " << complaints[i].category << endl; 
            cout << "Problem: " << complaints[i].problem << endl; 
            cout << "Status: " << complaints[i].status << endl; 
 
            found=true; 
        } 
    } 
 
    if(!found) 
    cout << "\nNo complaint found for this Enrollment Number\n"; 
} 
int main() { 
 
    vector<Complaint> complaints; 
    int choice; 
 
    do { 
 
        showMenu(); 
        cin >> choice; 
 
        switch(choice) { 
 
            case 1: 
 
 
 
                submitComplaint(complaints); 
                break; 
 
            case 2: 
                viewComplaints(complaints); 
                break; 
 
            case 3: 
                searchComplaint(complaints); 
                break; 
 
            case 4: 
                cout << "\nExiting System...\n"; 
                break; 
 
            default: 
                cout << "\nInvalid Choice\n"; 
        } 
 
    } while(choice!=4); 
 
    return 0; 
}
