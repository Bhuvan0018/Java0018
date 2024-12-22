import java.util.*;

class Book {
    private String title;
    private String author;
    private String isbn;
    private boolean isIssued;

    public Book(String title, String author, String isbn) {
        this.title = title;
        this.author = author;
        this.isbn = isbn;
        this.isIssued = false;
    }

    public String getTitle() {
        return title;
    }

    public String getAuthor() {
        return author;
    }

    public String getIsbn() {
        return isbn;
    }

    public boolean isIssued() {
        return isIssued;
    }

    public void issueBook() {
        if (!isIssued) {
            isIssued = true;
            System.out.println("Book issued successfully.");
        } else {
            System.out.println("This book is already issued.");
        }
    }

    public void returnBook() {
        if (isIssued) {
            isIssued = false;
            System.out.println("Book returned successfully.");
        } else {
            System.out.println("This book was not issued.");
        }
    }

    public void displayBookInfo() {
        System.out.println("Title: " + title + ", Author: " + author + ", ISBN: " + isbn + ", Issued: " + (isIssued ? "Yes" : "No"));
    }
}

class Member {
    private String name;
    private int memberId;
    private List<Book> issuedBooks;

    public Member(String name, int memberId) {
        this.name = name;
        this.memberId = memberId;
        this.issuedBooks = new ArrayList<>();
    }

    public String getName() {
        return name;
    }

    public int getMemberId() {
        return memberId;
    }

    public void issueBook(Book book) {
        if (!book.isIssued()) {
            book.issueBook();
            issuedBooks.add(book);
        } else {
            System.out.println("The book is already issued to someone else.");
        }
    }

    public void returnBook(Book book) {
        if (issuedBooks.contains(book)) {
            book.returnBook();
            issuedBooks.remove(book);
        } else {
            System.out.println("This book was not issued to you.");
        }
    }

    public void displayIssuedBooks() {
        if (issuedBooks.isEmpty()) {
            System.out.println(name + " has no issued books.");
        } else {
            System.out.println(name + " has the following issued books:");
            for (Book book : issuedBooks) {
                book.displayBookInfo();
            }
        }
    }
}

class Library {
    private List<Book> books;
    private List<Member> members;

    public Library() {
        books = new ArrayList<>();
        members = new ArrayList<>();
    }

    public void addBook(Book book) {
        books.add(book);
        System.out.println("Book added: " + book.getTitle());
    }

    public void removeBook(Book book) {
        if (books.contains(book)) {
            books.remove(book);
            System.out.println("Book removed: " + book.getTitle());
        } else {
            System.out.println("Book not found in library.");
        }
    }

    public void addMember(Member member) {
        members.add(member);
        System.out.println("Member added: " + member.getName());
    }

    public void removeMember(Member member) {
        if (members.contains(member)) {
            members.remove(member);
            System.out.println("Member removed: " + member.getName());
        } else {
            System.out.println("Member not found.");
        }
    }

    public void issueBookToMember(Book book, Member member) {
        if (books.contains(book)) {
            member.issueBook(book);
        } else {
            System.out.println("Book not available in library.");
        }
    }

    public void returnBookFromMember(Book book, Member member) {
        member.returnBook(book);
    }

    public void showAllBooks() {
        if (books.isEmpty()) {
            System.out.println("No books available in the library.");
        } else {
            System.out.println("All books in the library:");
            for (Book book : books) {
                book.displayBookInfo();
            }
        }
    }

    public void showAllMembers() {
        if (members.isEmpty()) {
            System.out.println("No members in the library.");
        } else {
            System.out.println("All library members:");
            for (Member member : members) {
                System.out.println("Member Name: " + member.getName() + ", Member ID: " + member.getMemberId());
            }
        }
    }
}

public class LibraryManagementSystem {
    public static void main(String[] args) {
        Library library = new Library();

        // Adding books to the library
        Book book1 = new Book("The Great Gatsby", "F. Scott Fitzgerald", "123456");
        Book book2 = new Book("1984", "George Orwell", "654321");
        Book book3 = new Book("To Kill a Mockingbird", "Harper Lee", "112233");

        library.addBook(book1);
        library.addBook(book2);
        library.addBook(book3);

        // Adding members
        Member member1 = new Member("Alice", 101);
        Member member2 = new Member("Bob", 102);
        library.addMember(member1);
        library.addMember(member2);

        // Display all books in the library
        library.showAllBooks();

        // Issue books to members
        library.issueBookToMember(book1, member1);
        library.issueBookToMember(book2, member2);

        // Display issued books
        member1.displayIssuedBooks();
        member2.displayIssuedBooks();

        // Return books
        library.returnBookFromMember(book1, member1);
        library.returnBookFromMember(book2, member2);

        // Display all books after returning
        library.showAllBooks();

        // Removing books and members
        library.removeBook(book3);
        library.removeMember(member2);

        // Display all books and members after removal
        library.showAllBooks();
        library.showAllMembers();
    }
}
