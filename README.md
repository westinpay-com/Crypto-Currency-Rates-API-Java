# Crypto-Currency-Rates-API-Java
This repository is used to retrieve the list of currencies using WestinPay's API which provides the list of currencies.
## WestinPay Crypto Currency Java Code

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class Main {
    public static void main(String[] args) {
        String apiKey = "your_api_key";
        String base = "BTC";
        String output = "JSON";
        String urlString = "https://westinpay.com/currency/crypto_api?api_key=" + apiKey + "&base=" + base + "&output=" + output;

        try {
            URL url = new URL(urlString);
            HttpURLConnection conn = (HttpURLConnection) url.openConnection();
            conn.setRequestMethod("GET");

            int responseCode = conn.getResponseCode();
            if (responseCode == HttpURLConnection.HTTP_OK) {
                BufferedReader in = new BufferedReader(new InputStreamReader(conn.getInputStream()));
                String inputLine;
                StringBuffer response = new StringBuffer();

                while ((inputLine = in.readLine()) != null) {
                    response.append(inputLine);
                }
                in.close();

                System.out.println(response.toString());
            } else {
                System.out.println("GET request not worked");
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
