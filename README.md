# Crypto-Currency-Rates-API-Java
This repository is used to retrieve the list of currencies using WestinPay's API which provides the list of currencies.


WestinPay's Free Crypto Currency API provides real-time exchange rates and currency conversion for all cryptocurrencies. It's ideal for financial apps, e-commerce platforms, and travel services.

## Endpoint

The WestinPay Crypto Currency Endpoint delivers real-time exchange rates.

### Authentication

Once you have created an account on [WestinPay](https://westinpay.com/merchant/register), your account will be assigned a unique 32-character API key. Think of this like a secure password; keep it safe and do not share it with others.

### Getting Your API Key

After registering, go to the dashboard and navigate to the "Currency Key" section. Here, you can generate your Fiat API key. This key is essential for authenticating your requests to the API.

### Parameters

- **base**: The base currency for conversion. Default is BTC. // For other currencies, use the currency symbol e.g. base=USDT
- **output**: Response format, either JSON or XML. Default is JSON.
- **api_key**: Your unique API key. Replace YOUR-API-KEY with your actual API key.

### Usage Limitations

Please note that your API key allows for up to 5000 monthly requests. This limit is automatically renewed each month. It's important to manage your usage to ensure continuous access to the API.
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
