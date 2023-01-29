## Lab Report 2 - Servers and Bugs

# String Server

Here is my code for my string server, which supports the specified behaviour from the course site:
```java
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {
    String cur;
    Handler(){
        cur = new String();
    }
    public String handleRequest(URI url) {
        if (url.getPath().equals("/add-message")) {
            String[] p = url.getQuery().split("=");  
            if(!p[0].equals("s")){
                return "Invalid Query";
            }
            cur += p[1] + "\n"; 
            return cur;
        } else {
            return "404 Not Found!";
        }
    }
}

class StringServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}
```
I made it by modifying the number server template, so much of the boilerplate code was unchanged. 

Here are some examples of using `/add-message': 

![sus](https://s.fft.ac/L42sgK/direct)

Here, the `handleRequest` method was called by the `Server` class to handle the request. The argument to `handleRequest` was `/add-message?s=sus` -- I queried '/add-message' with `s = sus`. Then, the code called various helper methods to parse the url. For example, it called `getPath` and `equals` with the argument of `/add-message` in order to determine if the path was correct. And it used `.split` with the `=` argument to parse the value for the query. 

In the end, the instance variable `String cur` was appended to with the input string plus a newline character `\n`. Then, `cur` was returned as the result of `handleRequest`, and it was printed to the browser. 

![amogus](https://s.fft.ac/lLvEXk/direct)

The methods called for this query are the same as the previous one. The only difference is that `cur` contained the value `sus\n` from the previous query, so when it was appended with the current input string, it became `sus\namogus\n`, and hence the output to the browser was: 

```
sus
amogus
```

