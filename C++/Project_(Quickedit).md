```
#include <iostream>
#include <stack>
#include <fstream>
#include <string>
#include <cstdio>
using namespace std;

// Node structure for Doubly Linked List
struct Node {
    string data;
    Node* prev;
    Node* next;

    Node(string str) : data(str), prev(nullptr), next(nullptr) {}
};

// Text Editor class
class TextEditor {
private:
    Node* head;
    Node* tail;
    Node* cursor; // Cursor position
    stack<string> undoStack, redoStack;
    string clipboard; // Copy-paste clipboard

public:
    TextEditor() : head(nullptr), tail(nullptr), cursor(nullptr) {}

    // Helper function to get current text as string
    string getCurrentText() {
        string text;
        Node* temp = head;
        while (temp) {
            text += temp->data + " ";
            temp = temp->next;
        }
        return text;
    }

    // Restore text from saved state
    void restoreText(const string& state) {
        clearText(); // Clear existing text
        string word;
        for (char ch : state) {
            if (ch == ' ') {
                if (!word.empty()) {
                    insertWord(word);
                    word.clear();
                }
            } else {
                word += ch;
            }
        }
        if (!word.empty()) insertWord(word);
    }

    // Clear the text editor
    void clearText() {
        while (head) {
            Node* temp = head;
            head = head->next;
            delete temp;
        }
        tail = cursor = nullptr;
    }

    // Save current state to undo stack
    void saveState() {
        undoStack.push(getCurrentText());
        while (!redoStack.empty()) redoStack.pop(); // Clear redo stack on new change
    }

    // Undo last operation
    void undo() {
        if (!undoStack.empty()) {
            redoStack.push(getCurrentText());
            restoreText(undoStack.top());
            undoStack.pop();
            cout << "Undo successful." << endl;
        } else {
            cout << "Nothing to undo!" << endl;
        }
    }

    // Redo last undone operation
    void redo() {
        if (!redoStack.empty()) {
            undoStack.push(getCurrentText());
            restoreText(redoStack.top());
            redoStack.pop();
            cout << "Redo successful." << endl;
        } else {
            cout << "Nothing to redo!" << endl;
        }
    }

    // Insert multiple words at cursor position
    void insertText(const string& text) {
        saveState();
        string word;
        for (char ch : text) {
            if (ch == ' ') {
                if (!word.empty()) {
                    insertWord(word);
                    word.clear();
                }
            } else {
                word += ch;
            }
        }
        if (!word.empty()) insertWord(word);
    }

    // Insert a single word at cursor position
    void insertWord(const string& word) {
        Node* newNode = new Node(word);
        if (!head) {
            head = tail = cursor = newNode;
        } else {
            if (!cursor) {
                newNode->next = head;
                head->prev = newNode;
                head = cursor = newNode;
            } else {
                newNode->prev = cursor;
                newNode->next = cursor->next;
                if (cursor->next) cursor->next->prev = newNode;
                cursor->next = newNode;
                if (!newNode->next) tail = newNode;
                cursor = newNode;
            }
        }
    }

    // Clear the text editor (new file)
    void newFile() {
        clearText();
        while (!undoStack.empty()) undoStack.pop();
        while (!redoStack.empty()) redoStack.pop();
        cout << "New file created." << endl;
    }

    // Open a file and load its content
    void openFile() {
        cout << "Enter filename to open: ";
        string filename;
        cin >> filename;
        ifstream file(filename);
        if (file.is_open()) {
            newFile();
            string word;
            while (file >> word) {
                insertWord(word);
            }
            file.close();
            cout << "File opened successfully!" << endl;
        } else {
            cout << "Error opening file!" << endl;
        }
    }

    // Copy text from cursor position to clipboard
    void copyText() {
        if (cursor) {
            clipboard = cursor->data;
            cout << "Copied: " << clipboard << endl;
        } else {
            cout << "Nothing to copy!" << endl;
        }
    }

    // Paste text from clipboard at cursor position
    void pasteText() {
        if (!clipboard.empty()) {
            insertText(clipboard);
            cout << "Pasted: " << clipboard << endl;
        } else {
            cout << "Clipboard is empty!" << endl;
        }
    }

    // Save text to a file
    void saveToFile() {
        cout << "Enter filename to save: ";
        string filename;
        cin >> filename;
        ofstream file(filename);
        if (file.is_open()) {
            file << getCurrentText();
            file.close();
            cout << "File saved successfully!" << endl;
        } else {
            cout << "Error saving file!" << endl;
        }
    }

    // Delete file from the system
    void deleteFile() {
        cout << "Enter filename to delete: ";
        string filename;
        cin >> filename;
        if (remove(filename.c_str()) == 0) {
            cout << "File deleted successfully!" << endl;
        } else {
            cout << "Error deleting file!" << endl;
        }
    }

    // Display the entire text
    void displayText() {
        Node* temp = head;
        while (temp) {
            cout << temp->data << " ";
            temp = temp->next;
        }
        cout << endl;
    }

    // Edit existing text
    void editText() {
        cout << "Enter new text: ";
        string newText;
        getline(cin, newText);
        newFile(); // Clear the current text
        insertText(newText); // Insert the new text
    }
};

int main() {
    TextEditor editor;
    string command;

    cout << "Simple Text Editor (Type 'h' for help)\n";

    while (true) {
        cout << "Enter command: ";
        cin >> command;
        cin.ignore();

        if (command == "n") {
            editor.newFile();
        } else if (command == "e") {
            editor.editText();
        } else if (command == "o") {
            editor.openFile();
        } else if (command == "c") {
            editor.copyText();
        } else if (command == "v") {
            editor.pasteText();
        } else if (command == "p") {
            editor.displayText();
        } else if (command == "s") {
            editor.saveToFile();
        } else if (command == "d") {
            editor.deleteFile();
        } else if (command == "h") {
            cout << "Commands: n (new), e (edit), o (open), c (copy), v (paste), p (print), s (save), d (delete file), h (help), q (quit)\n";
        } else if (command == "q") {
            break;
        } else {
            cout << "Invalid command! Type 'h' for help.\n";
        }
    }
    return 0;
}
```
