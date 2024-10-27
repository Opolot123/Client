import java.net.URL;
import java.net.HttpURLConnection;
import java.util.Scanner;

// Client to view available books
public class ViewBooksClient {
    public static void main(String[] args) throws Exception {
        // Sending a GET request to the server to view available books
        URL url = new URL("http://localhost:8080/api/books");
        HttpURLConnection conn = (HttpURLConnection) url.openConnection();
        conn.setRequestMethod("GET"); // Specify the request method

        // Reading the response
        if (conn.getResponseCode() == 200) {
            Scanner scanner = new Scanner(url.openStream());
            while (scanner.hasNext()) {
                System.out.println(scanner.nextLine()); // Print the list of available books
            }
            scanner.close(); // Close the scanner
        } else {
            System.out.println("Failed to retrieve books. Response Code: " + conn.getResponseCode());
        }
    }
}
