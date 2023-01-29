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
I made it by modifying the number server template, so smuch of the boilerplate code was unchanged. 
