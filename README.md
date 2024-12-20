# burp_bambdas
Collection of useful bambdas, that is used to filter interesting things in Burp Suite


## What is bambdas?
Portswigger have a lot of useful information about bambdas and how to find it in the application, [Link](https://portswigger.net/burp/documentation/desktop/tools/proxy/http-history/bambdas)

They also have a looooong list with [filters](https://github.com/PortSwigger/bambdas/tree/main/Filter/Proxy/HTTP) 

Bambdas is basically Java-code used as filters for different things, such as in the HTTP History, but it is also possible to create custom columns in the HTTP History. 

## Useful bambdas
This is a collection of bambdas that I find useful in my daily work

### Highlight requests that are edited
```
if (requestResponse.edited()) {
     requestResponse.annotations().setHighlightColor(HighlightColor.CYAN);
}

return true;
```

> There are several colors to choose from. When the dot is printed after HighlightColor there will suggestions of what colors to use.

### Highlight requests that uses http (not-secure)
```
var request = requestResponse.request();
var requestUrl = request.url();

if (requestUrl.startsWith("http://")) {
	requestResponse.annotations().setHighlightColor(HighlightColor.ORANGE);
}

return true;
```

### Highlight all requests that contains specific word and is within the defined scope 
```
if(requestResponse.request().contains("useful-text-here", true)){
 requestResponse.annotations().setHighlightColor(HighlightColor.MAGENTA);   
    
}

return requestResponse.request().isInScope() == true;
```

### Combined filters: Highlight all requests that uses http (filter 1) and all requets that have specific words (filter 2)
```
var request = requestResponse.request();
var requestUrl = request.url();

if (requestUrl.startsWith("http://")) {
	requestResponse.annotations().setHighlightColor(HighlightColor.ORANGE);
}


if(requestResponse.request().contains("first-interesting-word", true) || requestResponse.request().contains("second-interesting-word", true)){
 requestResponse.annotations().setHighlightColor(HighlightColor.MAGENTA);   
    
}

return true;
```

### Only show requests that have a redirect response 
```
if (!requestResponse.hasResponse()) {
    return false;
    }

var response = requestResponse.response();
return response.isStatusCodeClass(StatusCodeClass.CLASS_3XX_REDIRECTION);
```

> There are several StatusCodeClasses to choose from. When the dot is printed after StatusCodeClass there will be suggestions of what types to use.



## Add custom colums in HTTP History using bambdas
Official guide at [Portswigger](https://portswigger.net/burp/documentation/desktop/tools/proxy/http-history#adding-a-custom-column)

To create a custom column for your HTTP history table:

1. In **Proxy > HTTP History**, click the options menu  **> Add custom column**. The **Add custom column** window opens.
2. Enter a name for your custom column in the **Column header** field.
3. Write a Bambda to specify the data that the custom column displays.

### Create a custom column with content of the Server-header
```
return requestResponse.hasResponse() && requestResponse.response().hasHeader("Server")
  ? requestResponse.response().headerValue("Server")
  : "";
```
