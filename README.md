# WillowHome
Demonstrate how to read the contents of a text file using C++. Demonstrate how to search the data in a file. Demonstrate how to create a new file using C++. Demonstrate how to write to a file using C++. Demonstrate how to write the contents from a file to the display. Demonstrate how to write the contents from the display to a file.
/* Sanyerlis Camacaro- CSC275 - Sancamac@uat.edu Assignment: File I/O Google Home
This code demonstrates how to:

Read the contents of a text file using C++ (recall function).
Search the data in a file (search function).
Create a new file using C++ (when the file is opened for the first time in the remember function).
Write to a file using C++ (remember function).
Write the contents from a file to the display (when recalling/searching data).
Write the contents from the display to a file (when remembering data).
The "WillowHome" device has a simple text-based interface and a friendly personality. 
It can remember and recall data, and it provides a good user experience through clear 
instructions and helpful output. */

#include <iostream> // includes input and out as the standard library.
#include <fstream> // it provides the capability of creating, writing and reading a file. 
#include <string> // this allows me to work with strings.
#include <vector> // telling the compiler to not only use your own code, but to also compile a file called vector.

using namespace std; // means using standard namespace and that I dont have to type std:: in front of each line.

// Function to write data to a file
void remember(string data) {
    ofstream outFile("WillowHomeData.txt", ios::app);
    outFile << data << endl;
    outFile.close();
}


// Function to read data from a file

vector<string> recall() {
    vector<string> data;
    string line;
    ifstream inFile("WillowHomeData.txt");

    while (getline(inFile, line)) {
        data.push_back(line);
    }
    inFile.close();
    return data;
}

// Function to search data in a file

vector<string> search(string query) {

    vector<string> data = recall();

    vector<string> results;

    for (const auto& line : data) {

        if (line.find(query) != string::npos) {

            results.push_back(line);

        }

    }

    return results;

}

// Main function
int main() {

    cout << "\nWelcome to WillowHome, your text-based assistant!\n" << endl;

    cout << "\nWillowHome can remember and recall things for you.\n" << endl;



    string input;

    while (true) {

        cout << "\nEnter a command (remember/recall/search/exit): \n";

        getline(cin, input);



        if (input == "remember") {

            cout << "What do you want me to remember? ";

            getline(cin, input);

            remember(input);

            cout << "I have remembered: " << input << endl;

        }
        else if (input == "recall") {

            cout << "Recalling all items: " << endl;

            vector<string> data = recall();

            for (const auto& item : data) {

                cout << item << endl;

            }

        }
        else if (input == "search") {

            cout << "Enter search query: ";

            getline(cin, input);

            vector<string> results = search(input);

            if (results.empty()) {

                cout << "No results found for: " << input << endl;

            }
            else {

                cout << "Search results for '" << input << "':" << endl;

                for (const auto& item : results) {

                    cout << item << endl;

                }

            }

        }
        else if (input == "exit") {

            cout << "Goodbye! Have a great day!" << endl;

            break;

        }
        else {

            cout << "Invalid command. Please try again." << endl;

        }

    }



    return 0;

}
