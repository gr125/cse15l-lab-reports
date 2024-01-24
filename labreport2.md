# Lab Report 2

## Part 1

Code for `ChatServer`:
```
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
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

Adding a message: 
![](/labreport2_screenshots/addmessage1.png)
Adding another message:
![](/labreport2_screenshots/addmessage2.png)

## Part 2

**Private key's absolute path**
![](/labreport2_screenshots/privatekeypath.png)
This screenshot shows the absolute path of the private SSH key located on my local computer. The terminal on the left shows the generation of the key and gives its path as `/Users/gauri/.ssh/id_rsa.pub`. The terminal on the right shows the process of navigating to the path of the private SSH key from the home directory of `/Users/gauri`. Once in the `.ssh/` directory, the `ls` commands shows the `id_rsa.pub` file, where the key is stored. 

**Public key's absolute path**
![](/labreport2_screenshots/publickeypath.png)
This screenshot shows the process of navigating to the path of the public SSH key when in `ieng6`'s file system. After entering the `.ssh` directory, the `ls` command shows the `authorized_keys` file, which is where the key is stored. 

**Logging into `ieng` without a password**
![](/labreport2_screenshots/sshnopassword.png)

## Part 3
