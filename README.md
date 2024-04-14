#include <iostream>
#include <string>
#include <map>

using namespace std;

string caesar_enc(string text, int s) {
    string result = "";
    for (int i = 0; i < text.length(); i++) {
        if (isupper(text[i])) {
            result += char((int(text[i] - 'A' + s) % 26 + 26) % 26 + 'A');
        } else if (islower(text[i])) {
            result += char((int(text[i] - 'a' + s) % 26 + 26) % 26 + 'a');
        } else {
            result += text[i];  // Handle non-alphabet characters
        }
    }
    return result;
}

string caesar_dec(string text, int s) {
    // Decryption is the same as encryption with a negative shift
    return caesar_enc(text, -s);
}

int main() {
    map<string, string> user_data;

    while (true) {
        cout << "__________" << endl;
        cout << "|___ 1.REGISTER ___|" << endl;
        cout << "|___ 2.LOGIN ____|" << endl;
        cout << "|___ 3.QUIT _____|" << endl;

        int choice;
        cin >> choice;

        if (choice == 1) {
            string username, password;
            cout << "Enter your username: ";
            cin >> username;
            cout << "Enter your password: ";
            cin >> password;
            user_data[username] = password;
            cout << "REGISTRATION SUCCESSFUL. YOUR PASSWORD IS: " << password << endl;
        } else if (choice == 2) {
            string username, password;
            cout << "Enter your username: ";
            cin >> username;
            cout << "Enter your password: ";
            cin >> password;

            if (user_data.find(username) != user_data.end() && user_data[username] == password) {
                cout << "Login Successful." << endl;

                while (true) {
                    cout << "__________" << endl;
                    cout << "___ 1.ENCRYPT ____" << endl;
                    cout << "___ 2.DECRYPT ____" << endl;
                    cout << "___ 3.LOGOUT  ____" << endl;

                    int sub_choice;
                    cin >> sub_choice;

                    if (sub_choice == 1) {
                        string message;
                        cout << "Enter the message to Encrypt: ";
                        cin.ignore();
                        getline(cin, message);

                        cout << "\nEnter the Caesar Cipher shift: ";
                        int shift;
                        cin >> shift;
                        string encrypted_message = caesar_enc(message, shift);
                        cout << "Encrypted message: " << encrypted_message << endl;
                    } else if (sub_choice == 2) {
                        string encrypted_message;
                        cout << "Enter the message to decrypt: ";
                        cin.ignore();
                        getline(cin, encrypted_message);

                        cout << "Enter the Caesar Cipher shift: ";
                        int shift;
                        cin >> shift;
                        string decrypted_message = caesar_dec(encrypted_message, shift);
                        cout << "Decrypted message: " << decrypted_message << endl;
                    } else if (sub_choice == 3) {
                        cout << "Logged out." << endl;
                        break;
                    } else {
                        cout << "Invalid option. Please try again." << endl;
                    }
                }
            } else {
                cout << "Invalid username or password. Please try again." << endl;
            }
        } else if (choice == 3) {
            cout << "Goodbye!" << endl;
            break;
        } else {
            cout << "Invalid option. Please try again." << endl;
        }
    }

    return 0;
}
