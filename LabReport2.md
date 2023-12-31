# Lab Report 2
---

# Part 1
### StringServer.java code: 
``` Java
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;

class Handler implements URLHandler { 
    ArrayList<String> queries = new ArrayList<String>();
    String output = "";
    public String handleRequest(URI url) {
        if (url.getPath().equals("/add-message")) {
            String[] parameters = url.getQuery().split("=");
            if(parameters[0].equals("s")) {
                queries.add(parameters[1]);
                if(queries.size()>1){
                    output+= "\n" + queries.size() + ". " + queries.get(queries.size()-1);
                }
                else {
                    output+= "1. " + queries.get(0);
                }
            }
            return output;
        } 
        else{
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
### Screenshots: 


![image](https://github.com/ssarahjackson/cse15l-lab-reports/assets/46005666/12ce918a-340e-4bfa-9569-99325bf682df)

Here the code started by running the `main` method in StringServer, which then called Server.java's (the included Server class from Lab 2) `start` method. The `start` method requires a `port` number given by user input, and in this screenshot I provided 5000 as the `port` number. Additionally, the `start` method creates an instance of a Handler class as its second argument. The `start` method then creates an instance of the HttpServer class and uses that class's `createContext` and `start` methods. Eventually, the `handleRequest` method I created in StringServer.java gets called, which takes a `url` variable as an argument which will be the link to the webpage. This `url` gets split up by this method based on its path and query, which in this example are add-message and hi respectively. Since `handleRequest` has not been called yet, the ArrayList `queries` and String `output` are empty. However, as we split up the `url`, `queries` will have a String "hi" added to it, and the String we return,`output`, will become "1. hi" as there's only one value in `queries`. 


![image](https://github.com/ssarahjackson/cse15l-lab-reports/assets/46005666/1df73b1e-bf64-417e-b1e3-0e68e6eb6def)

The code functions the exact same as the previous screenshot up until the `handleRequest` method (still taking `url` as an argument) gets called. This time its `queries` variable already has an element "hi" and `output`'s value remains "1. hi" from when `handleRequest` was previously called in the above example. This time, the `url` gets processed the same way so `queries` gets the String "Nice to meet you" added as an element in the ArrayList. In addition, `output`'s value gets "\n2. Nice to meet you" concatenated onto the preexisting "1. hi". Altogether, this gives us `output` being the String "1. hi\n2. Nice to meet you" which then gets returned by the method. 



# Part 2

### `ls` to private key
![image](https://github.com/ssarahjackson/cse15l-lab-reports/assets/46005666/4a7efc78-aa4d-427d-9b86-795e4552c6e2)

In this screenshot, we can see the private key is the first result under the name "id_rsa".


### `ls` to public key on ieng6
![image](https://github.com/ssarahjackson/cse15l-lab-reports/assets/46005666/0967c9e5-4679-4d59-aa18-7e0e29a2699b)


### logging in without password prompt 
![image](https://github.com/ssarahjackson/cse15l-lab-reports/assets/46005666/1963df07-b773-4ee7-82d3-01da3ab92b45)


# Part 3

I had never accessed another computer remotely before without using some software that does it for you, so learning about ssh and other protocols was very cool and easier than I expected. I also had no clue how creating your own server worked so making the web servers and having them do different things based on the URL was new to me. I kind of picked up some of how URLs worked from some work I did in a software engineering class at my previous college, but I didn't formally learn it as we did in week 2.
