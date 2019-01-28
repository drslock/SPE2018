Spring & JSON API Exercise
--------------------------
.
#### Objective
When this session is over, we need to get out of here !  
Let's interrogate _The Bristol API_ to find out details of the next departing bus  

#### Register
First register with _The Bristol API_ at: https://portal-bristol.api.urbanthings.io/#/home  
You will need to confirm your email address via the email message you should have been sent  
On the website, add the Bristol (Transport) API to "Your APIs"  
Get the API key from the new email you have just been sent - you will need it in your code.  

Finally, take a look through and become familar with the API documentation:  
https://portal-bristol.api.urbanthings.io/scripts/swagger-ui/dist/index.html  

#### Project
Use initializr (https://start.spring.io) to create a template Spring application  
Create a Maven Java project with a suitable artifact name (e.g. "Bus")  
Be sure to add in the "Web" dependency !  

Note: Initializr doesn't incorporate the JSON-simple library  
You will have to add the dependency manually to your POM file:  

```xml
<dependency>
    <groupId>com.googlecode.json-simple</groupId>
    <artifactId>json-simple</artifactId>
    <version>1.1</version>
</dependency>
```

#### Basic Task
In your Spring code, write an HTTP request handler called _getBusStopID_  
For example: http://127.0.0.1:8080/getBusStopID?

This should return the Stop ID ("PrimaryCode") of the nearest bus stop.  
You will need to make use of the _/static/transitstops?_ API call from:  
https://bristol.api.urbanthings.io  

You will need to pass it your location (e.g. Lat: 51.455886, Long: -2.605178)  

Note _The Bristol API_ uses X-Api-Key Header Authentication  
So make use of the relevant HTTP request code from the lecture  
(this is provided at the end of this file for easy copy-and-paste !)  

You will need to make use of both _JSONArray_ and _JSONObject_  
Documentation for which you can find at:  
http://alex-public-doc.s3.amazonaws.com/json_simple-1.1/index.html  

#### Advanced Task
It would be nice to know when the next bus is from the bus stop !  
In your Spring code, write an HTTP request handler called _getNextBus_  
For example: http://127.0.0.1:8080/getNextBus?

You will need to make use of the real-time reporting features of the API  
In particular the _/rti/report?_ API call, passing it your Stop ID  
The returned JSON is fairly complex ! You will need to pull out:  
```
=> Data
    => RTIReports
        => The first element of the resulting array
            => UpcomingCalls
                => The first element of the resulting array
                    => ExpectedDepartureTime
```
You can choose which parser to use to do this: JSON-simple or JSONPath !

NOTE: Sometimes the Bristol API can be a bit patchy. If your query doesn't  
return a bus first time, try refreshing it after a couple of seconds  
(just to make sure ;o)


#### HTTP Request Code
```java
import java.io.*;
import java.util.*;
import java.net.*;
import org.json.simple.*;
import org.json.simple.parser.*;
import com.jayway.jsonpath.JsonPath;

private static JSONObject requestJSON(String urlString, String key)
{
    try {
        URL url = new URL(urlString);
        HttpURLConnection connection = (HttpURLConnection) url.openConnection();
        connection.setRequestMethod("GET");
        connection.setDoOutput(true);
        connection.setRequestProperty("X-Api-Key", key);
        InputStream stream = (InputStream) connection.getInputStream();
        JSONParser parser = new JSONParser();
        return (JSONObject)parser.parse(new InputStreamReader(stream, "UTF-8"));
    }
    catch(UnsupportedEncodingException uee) { return null; }
    catch(IOException ioe) { return null; }
    catch(ParseException pe) { return null; }
}

```