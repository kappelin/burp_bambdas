# burp_bambdas
Collection of useful bambdas, that is used to filter interesting things


## What is bambdas?
Portswigger have a lot of useful information about bambdas and how to find it in the application, [Link](https://portswigger.net/burp/documentation/desktop/tools/proxy/http-history/bambdas)

They also have a looooong list with filters [Link](https://github.com/PortSwigger/bambdas/tree/main/Filter/Proxy/HTTP) 

## Useful bambdas
This is a collection of bambdas that I find useful in my daily work

### Highlight requests that are edited
```
if (requestResponse.edited()) {
     requestResponse.annotations().setHighlightColor(HighlightColor.CYAN);
}
```


