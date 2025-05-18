

class Book {
    String id, title, author;
    boolean isIssued;

    Book(String id, String title, String author) {
        this.id = id;
        this.title = title;
        this.author = author;
        this.isIssued = false;
    }

    @Override
    public String toString() {
        return "ID: " + id + " | Title: " + title + " | Author: " + author + " | Issued: " + isIssued;
    }
}

public class LibrarySystem {
    static Map<String, Book> library = new HashMap<>();

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int choice;

        do {
            System.out.println("\nLibrary Menu:");
            System.out.println("1. Add Book");
            System.out.println("2. Issue Book");
            System.out.println("3. Return Book");
            System.out.println("4. View All Books");
            System.out.println("5. Exit");
            System.out.print("Enter choice: ");
            choice = sc.nextInt();
            sc.nextLine(); // consume newline

            switch (choice) {
                case 1 -> addBook(sc);
                case 2 -> issueBook(sc);
                case 3 -> returnBook(sc);
                case 4 -> viewBooks();
                case 5 -> System.out.println("Exiting...");
                default -> System.out.println("Invalid choice.");
            }
        } while (choice != 5);

        sc.close();
    }

    static void addBook(Scanner sc) {
        System.out.print("Enter Book ID: ");
        String id = sc.nextLine();
        if (library.containsKey(id)) {
            System.out.println("Book ID already exists.");
            return;
        }
        System.out.print("Enter Book Title: ");
        String title = sc.nextLine();
        System.out.print("Enter Author Name: ");
        String author = sc.nextLine();

        Book book = new Book(id, title, author);
        library.put(id, book);
        System.out.println("Book added successfully.");
    }

    static void issueBook(Scanner sc) {
        System.out.print("Enter Book ID to issue: ");
        String id = sc.nextLine();
        Book book = library.get(id);

        if (book == null) {
            System.out.println("Book not found.");
        } else if (book.isIssued) {
            System.out.println("Book is already issued.");
        } else {
            book.isIssued = true;
            System.out.println("Book issued successfully.");
        }
    }

    static void returnBook(Scanner sc) {
        System.out.print("Enter Book ID to return: ");
        String id = sc.nextLine();
        Book book = library.get(id);

        if (book == null) {
            System.out.println("Book not found.");
        } else if (!book.isIssued) {
            System.out.println("Book is not issued.");
        } else {
            book.isIssued = false;
            System.out.println("Book returned successfully.");
        }
    }

    static void viewBooks() {
        if (library.isEmpty()) {
            System.out.println("No books in the library.");
        } else {
            for (Book book : library.values()) {
                System.out.println(book);
            }
        }
    }
}
