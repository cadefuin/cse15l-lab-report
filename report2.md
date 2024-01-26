# Lab Report 2: Servers and SSH Keys (Week 3)
This lab consisted of creating a web server called `ChatServer` and exploring public/private keys for SSH.

## Part 1: ChatServer
The server was written by using the [wavelet server example](https://github.com/ucsd-cse15l-f23/wavelet) as a template. The entire folder was reused and unchanged, except the `NumberServer.java` file which was renamed to `ChatServer.java` and modified to contain the following classes:
```
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
```
class Handler implements URLHandler {
    //contains messages to display
    String display = "";

    public String handleRequest(URI url) {
        if(url.getPath().equals("/")) return display;
        else if (url.getPath().contains("/add-message")) {
            String[] parameters = url.getQuery().split("=");
            if (parameters[0].equals("s")) {
                String message = "";
                String user = "";
                String[]subParam = parameters[1].split("&");
                message = subParam[0];
                if(subParam[1].equals("user")) {
                    user = parameters[2];
                }
                return display += user + ": " + message + "\n";
            }
        }
        return "404 Not Found!";
    }
}
```
To start the server, the `main()` method in the `ChatServer` class was called with the argument `3579` to indicate the port on which to run the server. Then the `Server.start()` method was called with the port and a new `Handler` as arguments to specify the server's behavior.
An example of using `/add-message` can be seen below:<br><br>
![Example 1 of /add-message](cse15l-report-2-ss-1.png)<br><br>
Initially, the `display` value in `Handler` was an empty String. When the URL was inputted, the `handleRequest()` method was called with the URL as the argument. The `handleRequest()` method made local `message` and `user` variables from the URL, then concatenated these reformatted Strings to `display`. When `/add-message` was used again:<br><br>
![Example 2 of /add-message](cse15l-report-2-ss-2.png)<br><br>
The `handleRequest()` was called again with a different URL. New local `message` and `user` variables were derived from the new URL, then concatenated to `display`. The `display` String retained the previous message because it is an instance variable in the `Handler`. This means it does not reset to an empty string unless the server stops running.

## Part 2: Public/Private Keys
Private Key: <br><br>
![Absolute path to private key](cse15l-report-2-ss-3.png) <br><br>
Public Key: <br><br>
![Absolute path to public key](cse15l-report-2-ss-4.png) <br><br>
Log in without password: <br><br>
![Log in without password](cse15l-report-2-ss-5.png)

## Part 3: Reflection
In the past 2 weeks, my knowledge on servers has notably expanded: how a server actually works, how to set one up, and how to use related commands such as `ssh`, `scp`, and `mkdir`. Previously, I had a vague understanding of servers as a computer somehow involved in the interaction between other computers. Now I understand that servers store data and run commands received from other computers. The process of setting up a server and connecting to one via `ssh` was surprisingly simple, at least from the higher level that I observed in these labs. Although I already knew the concept of public and private keys in cybersecurity, the process of creating and copying them with `scp` and `mkdir` helped expand my understanding on where the keys are stored and how they are accessed.
