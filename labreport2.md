# Lab Report 2

## Part 1

**Code for `ChatServer.java`:**
```
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {
    // string containing all messages
    String S = "";

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            if (S.equals("")){
                return "No messages yet.";
            }
            else {
                return S;
            }
        }
        if (url.getPath().equals("/add-message")) {
            try{
                String[] parameters = url.getQuery().split("&");
                S += parameters[1].split("=")[1]+": "+parameters[0].split("=")[1] +"\n";
                return S;
            }
            catch (Exception E) {
                return "Incorrect query format.";
            }            
        } else {
            return "404 Not Found!";
        }
    }
}

class ChatServer {
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

**Adding a message:** 
![](/labreport2_screenshots/addmessage1.png)
- When `/add-message` is used, the `handleRequest()` method in the `Handler` class is called. 
- The `handleRequest()` method takes the page URL (a URI object) as an argument. 
- In the class, the string `S` contains all the messages that have been added; at this moment, the string is empty (`""`). 
- As a result of this request, the user and message from the query is added to the string `S` in the format `<user>: <message>\n`. The value of `S` changes from `""` to `"jpolitz: Hello"`
- First, the path is checked to include `/add-message` by checking the value returned by `getPath()`. Then, `getQuery()` gets the query component of `url` which is then split into the user and message components and stored in `parameters`. The values of `parameters` are further split to get the user and message (`"jpolitz"` and `"Hello"` respectively), which are then added to `S`. `S` is returned by the method resulting in `jpolitz: Hello` being displayed to the page. 

**Adding another message:**
![](/labreport2_screenshots/addmessage2.png)
- When `/add-message` is used, the `handleRequest()` method in the `Handler` class is called. 
- The `handleRequest()` method takes the page URL (a URI object) as an argument. 
- In the class, the string `S` contains all the messages that have been added (`"jpolitz: Hello\n"` since a message has already been added). 
- As a result of this request, the user and message from the query is added to the string `S` in the format `<user>: <message>\n`. The value of `S` changes from `"jpolitz: Hello\n"` to `"jpolitz: Hello\nyash: How+are+you"`
- First, the path is checked to include `/add-message` by checking the value returned by `getPath()`. Then, `getQuery()` gets the query component of `url` which is then split into the user and message components and stored in `parameters`. The values of `parameters` are further split to get the user and message (`"yash"` and `"How+are+you"` respectively), which are then added to `S`. `S` is returned by the method resulting in 
```
jpolitz: Hello
yash: How+are+you
``` 
being displayed to the page. 

## Part 2

**Private key's absolute path:** `/Users/gauri/.ssh/id_rsa.pub`
![](/labreport2_screenshots/privatekeypath.png)
This screenshot shows the absolute path of the private SSH key located on my local computer. The terminal on the left shows the generation of the key and gives its path as `/Users/gauri/.ssh/id_rsa.pub`. The terminal on the right shows the process of navigating to the path of the private SSH key from the home directory of `/Users/gauri`. Once in the `.ssh/` directory, the `ls` commands shows the `id_rsa.pub` file, where the key is stored. 

**Public key's absolute path:** `/home/linux/ieng6/oce/95/grenjith/.ssh/authorized_keys`
![](/labreport2_screenshots/publickeypath.png)
This screenshot shows the process of navigating to the path of the public SSH key when in `ieng6`'s file system. After entering the `.ssh` directory, the `ls` command shows the `authorized_keys` file, which is where the key is stored. 

**Logging into `ieng` without a password**
![](/labreport2_screenshots/sshnopassword.png)

## Part 3

From the lab in week 2, I learned how to work with URLs and process site queries. Using the `URI` class, you can get the path and query components of URLs and use that information to make changes (ex. in the `ChatServer` class the string containing the messages is manipulated). Using the `URLHandler` interface and the `Server` class, the week 2 lab task was to implement a simple search engine that could add text to a list and search for strings in that list. Specifically, I did not know that the parts of URLs (paths, queries) could be manipulated to implement functions that I have seen in many web pages. 