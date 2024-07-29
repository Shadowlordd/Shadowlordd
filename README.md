👋 Hola, soy @Shadowlordd
👀 Estoy interesado en todas las tecnologias
🌱 Actualmente estoy aprendiendo Programacion e ingenieria de sistemas
💞️ Estoy buscando colaborar en cualquier ambito de tecnologia
📫 Cómo llegar a mí, atraves de mi contacto de GMAIL: agust819@gmail.com
⚡ Dato curioso: tengo 21 años y domino varios lenguajes de programacion entre ellos:
c, c++, java, mysql, PHP, etc, tambien manejo RPG Maker, edicion de videos y Reparación de distintos dispositivos. 

Un ejemplo de proyecto:
---------Sistema de Gestión de Biblioteca-----------En lenguaje c----------

#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_BOOKS 100
#define MAX_USERS 50

typedef struct {
    char title[50];
    char author[50];
    char isbn[13];
    char category[30];
    int isBorrowed;
} Book;

typedef struct {
    char name[50];
    int userID;
    int borrowedBooks[MAX_BOOKS];
    int borrowedCount;
} User;

Book books[MAX_BOOKS];
User users[MAX_USERS];
int bookCount = 0;
int userCount = 0;

void addBook() {
    if (bookCount < MAX_BOOKS) {
        printf("Enter book title: ");
        scanf("%s", books[bookCount].title);
        printf("Enter book author: ");
        scanf("%s", books[bookCount].author);
        printf("Enter book ISBN: ");
        scanf("%s", books[bookCount].isbn);
        printf("Enter book category: ");
        scanf("%s", books[bookCount].category);
        books[bookCount].isBorrowed = 0;
        bookCount++;
        printf("Book added successfully!\n");
    } else {
        printf("Library is full!\n");
    }
}

void addUser() {
    if (userCount < MAX_USERS) {
        printf("Enter user name: ");
        scanf("%s", users[userCount].name);
        users[userCount].userID = userCount + 1;
        users[userCount].borrowedCount = 0;
        userCount++;
        printf("User added successfully!\n");
    } else {
        printf("User limit reached!\n");
    }
}

void borrowBook() {
    int userID, bookID;
    printf("Enter user ID: ");
    scanf("%d", &userID);
    printf("Enter book ID: ");
    scanf("%d", &bookID);

    if (userID <= userCount && bookID <= bookCount && !books[bookID - 1].isBorrowed) {
        users[userID - 1].borrowedBooks[users[userID - 1].borrowedCount] = bookID;
        users[userID - 1].borrowedCount++;
        books[bookID - 1].isBorrowed = 1;
        printf("Book borrowed successfully!\n");
    } else {
        printf("Invalid user ID or book ID, or book already borrowed!\n");
    }
}

void returnBook() {
    int userID, bookID;
    printf("Enter user ID: ");
    scanf("%d", &userID);
    printf("Enter book ID: ");
    scanf("%d", &bookID);

    if (userID <= userCount && bookID <= bookCount && books[bookID - 1].isBorrowed) {
        books[bookID - 1].isBorrowed = 0;
        for (int i = 0; i < users[userID - 1].borrowedCount; i++) {
            if (users[userID - 1].borrowedBooks[i] == bookID) {
                users[userID - 1].borrowedBooks[i] = users[userID - 1].borrowedBooks[users[userID - 1].borrowedCount - 1];
                users[userID - 1].borrowedCount--;
                break;
            }
        }
        printf("Book returned successfully!\n");
    } else {
        printf("Invalid user ID or book ID, or book not borrowed!\n");
    }
}

void listBooks() {
    for (int i = 0; i < bookCount; i++) {
        printf("Book ID: %d\n", i + 1);
        printf("Title: %s\n", books[i].title);
        printf("Author: %s\n", books[i].author);
        printf("ISBN: %s\n", books[i].isbn);
        printf("Category: %s\n", books[i].category);
        printf("Borrowed: %s\n", books[i].isBorrowed ? "Yes" : "No");
        printf("\n");
    }
}

void listUsers() {
    for (int i = 0; i < userCount; i++) {
        printf("User ID: %d\n", users[i].userID);
        printf("Name: %s\n", users[i].name);
        printf("Borrowed Books: ");
        for (int j = 0; j < users[i].borrowedCount; j++) {
            printf("%d ", users[i].borrowedBooks[j]);
        }
        printf("\n\n");
    }
}

int main() {
    int choice;
    while (1) {
        printf("Library Management System\n");
        printf("1. Add Book\n");
        printf("2. Add User\n");
        printf("3. Borrow Book\n");
        printf("4. Return Book\n");
        printf("5. List Books\n");
        printf("6. List Users\n");
        printf("7. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                addBook();
                break;
            case 2:
                addUser();
                break;
            case 3:
                borrowBook();
                break;
            case 4:
                returnBook();
                break;
            case 5:
                listBooks();
                break;
            case 6:
                listUsers();
                break;
            case 7:
                exit(0);
            default:
                printf("Invalid choice!\n");
        }
    }
    return 0;
}
