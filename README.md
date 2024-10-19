import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.OutputStream;
import java.net.HttpURLConnection;
import java.net.URL;

public class ItemClient {

    private static final String BASE_URL = "http://localhost:8080/items";

    public static void main(String[] args) throws Exception {
        createItem("Item 1");
        getAllItems();
        getItem(1L);
        updateItem(1L, "Updated Item 1");
        deleteItem(2L);
        getAllItems();
    }

    private static void getAllItems() throws Exception {
        HttpURLConnection connection = (HttpURLConnection) new URL(BASE_URL).openConnection();
        connection.setRequestMethod("GET");
        connection.setRequestProperty("Accept", "application/json");
        
        if (connection.getResponseCode() == 200) {
            BufferedReader in = new BufferedReader(new InputStreamReader(connection.getInputStream()));
            String inputLine;
            StringBuilder response = new StringBuilder();
            while ((inputLine = in.readLine()) != null) {
                response.append(inputLine);
            }
            in.close();
            System.out.println("All Items: " + response);
        }
    }

    private static void getItem(Long id) throws Exception {
        HttpURLConnection connection = (HttpURLConnection) new URL(BASE_URL + "/" + id).openConnection();
        connection.setRequestMethod("GET");
        
        // Handle response similar to getAllItems
    }

    private static void createItem(String name) throws Exception {
        HttpURLConnection connection = (HttpURLConnection) new URL(BASE_URL).openConnection();
        connection.setRequestMethod("POST");
        connection.setRequestProperty("Content-Type", "application/json");
        connection.setDoOutput(true);

        String jsonInputString = "{\"name\": \"" + name + "\"}";
        try (OutputStream os = connection.getOutputStream()) {
            byte[] input = jsonInputString.getBytes("utf-8");
            os.write(input, 0, input.length);
        }

        // Handle response
    }

    private static void updateItem(Long id, String newName) throws Exception {
        HttpURLConnection connection = (HttpURLConnection) new URL(BASE_URL + "/" + id).openConnection();
        connection.setRequestMethod("PUT");
        connection.setRequestProperty("Content-Type", "application/json");
        connection.setDoOutput(true);

        String jsonInputString = "{\"name\": \"" + newName + "\"}";
        try (OutputStream os = connection.getOutputStream()) {
            byte[] input = jsonInputString.getBytes("utf-8");
            os.write(input, 0, input.length);
        }

        // Handle response
    }

    private static void deleteItem(Long id) throws Exception {
        HttpURLConnection connection = (HttpURLConnection) new URL(BASE_URL + "/" + id).openConnection();
        connection.setRequestMethod("DELETE");
        
        // Handle response
    }
}
