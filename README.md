# Book-Shop-Management-System

import java.util.*;

class Author {
    private String name;
    private String email;

    public Author(String name, String email) {
        this.name = name;
        this.email = email;
    }

    public String getName() {
        return name;
    }

    public String getEmail() {
        return email;
    }
}

class Book {
    private String id;
    private String title;
    private Author author;
    private int numberOfCopies;

    public Book(String id, String title, Author author, int numberOfCopies) {
        this.id = id;
        this.title = title;
        this.author = author;
        this.numberOfCopies = numberOfCopies;
    }

    public String getId() {
        return id;
    }

    public String getTitle() {
        return title;
    }

    public Author getAuthor() {
        return author;
    }

    public int getNumberOfCopies() {
        return numberOfCopies;
    }

    public void setNumberOfCopies(int numberOfCopies) {
        this.numberOfCopies = numberOfCopies;
    }
}

class Bookstore {
    private Map<String, Book> books;

    public Bookstore() {
        books = new HashMap<>();
    }

    public void addBook(Book book) {
        books.put(book.getId(), book);
    }

    public void removeBook(String bookId) {
        books.remove(bookId);
    }

    public Book getBook(String bookId) {
        return books.get(bookId);
    }

    public List<Book> getAllBooks() {
        return new ArrayList<>(books.values());
    }
}

class AuthorManager {
    private Map<String, Author> authors;

    public AuthorManager() {
        authors = new HashMap<>();
    }

    public void addAuthor(Author author) {
        authors.put(author.getName(), author);
    }

    public void removeAuthor(String authorName) {
        authors.remove(authorName);
    }

    public Author getAuthor(String authorName) {
        return authors.get(authorName);
    }

    public List<Author> getAllAuthors() {
        return new ArrayList<>(authors.values());
    }
}

public class BookshopManagement {
    private Bookstore bookstore;
    private AuthorManager authorManager;

    public BookshopManagement() {
        bookstore = new Bookstore();
        authorManager = new AuthorManager();
    }

    public void controlPanel() {
        System.out.println("\t\t\t    OOP Project");
        System.out.println("\n\t\t\t Book Shop Management");
        System.out.println("\n\tGroup Members:  Zeeshan Haider , Dawood Khan");
        System.out.println("\n\t  Roll Number:   21-CP-24  ,    21-CP-100");
        System.out.println("\n\n\t\t\t\tCONTROL PANEL");
        System.out.println("1. ADD BOOK");
        System.out.println("2. DISPLAY BOOKS");
        System.out.println("3. CHECK PARTICULAR BOOK");
        System.out.println("4. UPDATE BOOK");
        System.out.println("5. DELETE BOOK");
        System.out.println("6. ADD AUTHOR");
        System.out.println("7. DISPLAY AUTHORS");
        System.out.println("8. EXIT");
    }

    public void addBook() {
        Scanner scanner = new Scanner(System.in);
        System.out.println("\n\n\t\t\t\tADD BOOKS");
        System.out.print("Book ID: ");
        String bookId = scanner.nextLine();
        System.out.print("Book Title: ");
        String bookTitle = scanner.nextLine();
        System.out.print("Author Name: ");
        String authorName = scanner.nextLine();
        System.out.print("Author Email: ");
        String authorEmail = scanner.nextLine();
        System.out.print("No. of Books: ");
        int numberOfCopies = scanner.nextInt();
        scanner.nextLine();

        Author author = authorManager.getAuthor(authorName);
        if (author == null) {
            author = new Author(authorName, authorEmail);
            authorManager.addAuthor(author);
        }

        Book book = new Book(bookId, bookTitle, author, numberOfCopies);
        bookstore.addBook(book);
    }

    public void showBooks() {
        System.out.println("\n\n\t\t\t\tAll BOOKS");
        List<Book> books = bookstore.getAllBooks();
        for (Book book : books) {
            System.out.println("Book ID: " + book.getId());
            System.out.println("Book Title: " + book.getTitle());
            System.out.println("Author Name: " + book.getAuthor().getName());
            System.out.println("Author Email: " + book.getAuthor().getEmail());
            System.out.println("No. of Books: " + book.getNumberOfCopies());
            System.out.println();
        }
        if (books.isEmpty()) {
            System.out.println("No books found.");
        }
    }

    public void checkBook() {
        Scanner scanner = new Scanner(System.in);
        System.out.println("\n\n\t\t\t\tCheck Particular Book");
        System.out.print("Book ID: ");
        String bookId = scanner.nextLine();

        Book book = bookstore.getBook(bookId);
        if (book != null) {
            System.out.println("Book ID: " + book.getId());
            System.out.println("Book Title: " + book.getTitle());
            System.out.println("Author Name: " + book.getAuthor().getName());
            System.out.println("Author Email: " + book.getAuthor().getEmail());
            System.out.println("No. of Books: " + book.getNumberOfCopies());
        } else {
            System.out.println("Book ID Not Found...");
        }
    }

    public void updateBook() {
        Scanner scanner = new Scanner(System.in);
        System.out.println("\n\n\t\t\t\tUpdate Book Record");
        System.out.print("Book ID: ");
        String bookId = scanner.nextLine();

        Book book = bookstore.getBook(bookId);
        if (book != null) {
            System.out.print("New Book Title: ");
            String newTitle = scanner.nextLine();
            System.out.print("New Author Name: ");
            String newAuthorName = scanner.nextLine();
            System.out.print("New Author Email: ");
            String newAuthorEmail = scanner.nextLine();
            System.out.print("New No. of Books: ");
            int newNumberOfCopies = scanner.nextInt();
            scanner.nextLine();

            Author author = authorManager.getAuthor(newAuthorName);
            if (author == null) {
                author = new Author(newAuthorName, newAuthorEmail);
                authorManager.addAuthor(author);
            }

            book.setNumberOfCopies(newNumberOfCopies);

            System.out.println("Book updated successfully.");
        } else {
            System.out.println("Book ID Not Found...");
        }
    }

    public void deleteBook() {
        Scanner scanner = new Scanner(System.in);
        System.out.println("\n\n\t\t\t\tDelete a Book");
        System.out.print("Book ID: ");
        String bookId = scanner.nextLine();

        Book book = bookstore.getBook(bookId);
        if (book != null) {
            bookstore.removeBook(bookId);
            System.out.println("Book is Deleted Successfully...");
        } else {
            System.out.println("Book ID Not Found...");
        }
    }

    public void addAuthor() {
        Scanner scanner = new Scanner(System.in);
        System.out.println("\n\n\t\t\t\tADD AUTHORS");
        System.out.print("Author Name: ");
        String authorName = scanner.nextLine();
        System.out.print("Author Email: ");
        String authorEmail = scanner.nextLine();

        Author author = new Author(authorName, authorEmail);
        authorManager.addAuthor(author);
    }

    public void showAuthors() {
        System.out.println("\n\n\t\t\t\tAll AUTHORS");
        List<Author> authors = authorManager.getAllAuthors();
        for (Author author : authors) {
            System.out.println("Author Name: " + author.getName());
            System.out.println("Author Email: " + author.getEmail());
            System.out.println();
        }
        if (authors.isEmpty()) {
            System.out.println("No authors found.");
        }
    }

    public void run() {
        Scanner scanner = new Scanner(System.in);
        int choice;

        do {
            controlPanel();
            System.out.print("Enter your choice (1-8): ");
            choice = scanner.nextInt();
            scanner.nextLine();

            switch (choice) {
                case 1:
                    addBook();
                    break;
                case 2:
                    showBooks();
                    break;
                case 3:
                    checkBook();
                    break;
                case 4:
                    updateBook();
                    break;
                case 5:
                    deleteBook();
                    break;
                case 6:
                    addAuthor();
                    break;
                case 7:
                    showAuthors();
                    break;
                case 8:
                    System.out.println("\nThank you for using the Bookshop Management System!");
                    break;
                default:
                    System.out.println("\nInvalid choice. Please try again.");
            }
        } while (choice != 8);
    }

    public static void main(String[] args) {
        BookshopManagement bookshopManagement = new BookshopManagement();
        bookshopManagement.run();
    }
}
