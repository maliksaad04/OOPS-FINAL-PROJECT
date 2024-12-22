#include <iostream>
#include <vector>
#include <string>
using namespace std;
// Book structure
struct Book {
    int id;
    string title;
    string author;
    bool isIssued;
    Book(int bookId, string bookTitle, string bookAuthor) : id(bookId), title(bookTitle), author(bookAuthor), isIssued(false) {}
};
// Member structure
struct Member {
    int id;
    string name;
    Member(int memberId, string memberName) : id(memberId), name(memberName) {}
};
class Library {
private:
    vector<Book> books;
    vector<Member> members;
public:
    // Add a new book
    void addBook(int id, string title, string author) {
        books.push_back(Book(id, title, author));
        cout << "Book added successfully!\n";
    }
    // View all books
    void viewBooks() {
        cout << "\nBooks in the Library:\n";
        for (const auto &book : books) {
            cout << "ID: " << book.id << ", Title: " << book.title << ", Author: " << book.author
                 << ", Issued: " << (book.isIssued ? "Yes" : "No") << endl;
        }
    }
    // Add a new member
    void addMember(int id, string name) {
        members.push_back(Member(id, name));
        cout << "Member added successfully!\n";
    }
    // View all members
    void viewMembers() {
        cout << "\nMembers in the Library:\n";
        for (const auto &member : members) {
            cout << "ID: " << member.id << ", Name: " << member.name << endl;
        }
    }
    // Issue a book
    void issueBook(int bookId) {
        for (auto &book : books) {
            if (book.id == bookId) {
                if (book.isIssued) {
                    cout << "Book is already issued!\n";
                    return;
                } else {
                    book.isIssued = true;
                    cout << "Book issued successfully!\n";
                    return;
                }
            }
        }
        cout << "Book not found!\n";
    }
    // Return a book
    void returnBook(int bookId) {
        for (auto &book : books) {
            if (book.id == bookId) {
                if (!book.isIssued) {
                    cout << "Book was not issued!\n";
                    return;
                } else {
                    book.isIssued = false;
                    cout << "Book returned successfully!\n";
                    return;
                }
            }
        }
        cout << "Book not found!\n";
    }
};
int main() {
    Library library;
    int choice;
    do {
        cout << "\nLibrary Management System\n";
        cout << "1. Add Book\n";
        cout << "2. View Books\n";
        cout << "3. Add Member\n";
        cout << "4. View Members\n";
        cout << "5. Issue Book\n";
        cout << "6. Return Book\n";
        cout << "7. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;
        switch (choice) {
            case 1: {
                int id;
                string title, author;
                cout << "Enter Book ID: ";
                cin >> id;
                cin.ignore();
                cout << "Enter Book Title: ";
                getline(cin, title);
                cout << "Enter Book Author: ";
                getline(cin, author);
                library.addBook(id, title, author);
                break;
            }
            case 2:
                library.viewBooks();
                break;
            case 3: {
                int id;
                string name;
                cout << "Enter Member ID: ";
                cin >> id;
                cin.ignore();
                cout << "Enter Member Name: ";
                getline(cin, name);
                library.addMember(id, name);
                break;
            }
            case 4:
                library.viewMembers();
                break;
            case 5: {
                int bookId;
                cout << "Enter Book ID to issue: ";
                cin >> bookId;
                library.issueBook(bookId);
                break;
            }
            case 6: {
                int bookId;
                cout << "Enter Book ID to return: ";
                cin >> bookId;
                library.returnBook(bookId);
                break;
            }
            case 7:
                cout << "Exiting...\n";
                break;
            default:
                cout << "Invalid choice!\n";
        }
    } while (choice != 7);

    return 0;
}

