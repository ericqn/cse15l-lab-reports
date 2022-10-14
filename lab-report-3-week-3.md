__Week 2 Lab Report Blog__

__Part 1__

The below code showcases the java file code for my SearchEngine.

```
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;


class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    int num = 0;

    String test = "Welcome to this webpage. You can start by using the commands add or search.";
    ArrayList<String> sList = new ArrayList<>();

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return test;
        } else if (url.getPath().equals("/increment")) {
            num += 1;
            return String.format("Number incremented!");
        } else {
            System.out.println("Path: " + url.getPath());
            if (url.getPath().contains("/add")) {
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("count")) {
                    num += Integer.parseInt(parameters[1]);
                    return String.format("Number increased by %s! It's now %d", parameters[1], num);
                }
                if (parameters[0].equals("s")) {
                    sList.add(parameters[1]);
                    return String.format("%s has been added to the list!", parameters[1]);
                }
            } else if (url.getPath().contains("/search")){
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("s")) {
                    ArrayList<String> sListModified = new ArrayList<>();
                    for(String s : sList) {
                        if(s.contains(parameters[1])) {
                            sListModified.add(s);
                        }
                    }

                    String toReturn = "";

                    for(String s : sListModified) {
                        toReturn = toReturn + " | "+ s;
                    }
                    return toReturn;
                }
            }
            return "404 Not Found!";
        }
    }

}

class SearchEngine {
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

Adding Items into the array:
![Image](lab3-screenshot1_1.png)

The method handleRequest is being called. In this case, the relevant values to this method are "/add", "s" and "pineapple". The argument "/add" is being detected by the url.contains method to call the specific command catered to the value "/add". The parameters array has the values "s" and "pineapples" input accordingly, where "s" represents that the value being used is a string and "pineapple" represents the string actually being input. When the method has been called, the "pineapple" string is added to the field sList.

![Image](lab3-screenshot1_2.png)

The method handleRequest is being called. In this case, the relevant values to this method are "/add", "s" and "apple". The parameters argument is used in a very similar fashion to the statement made above. When called, the value in the first index of parameters is changed from "pineapple" to "apple" to account for the update. When the method has been called, the "apple" string is added to the field sList.

![Image](lab3-screenshot1_3.png)

The method handleRequest is being called. In this case, the relevant values to this method are "/add", "s" and "banananana". The parameters argument is used in a very similar fashion to the statement made above. When called, the value in the first index of parameters is changed from "apple" to "banananana" to account for the update. When the method has been called, the "banananana" string is added to the field sList.

![Image](lab3-screenshot1_4.png)

The method handleRequest is being called. The relevant arguments is the parameters array. Being input as values into the array are "/search", "s", and "apple". The method updates the "/add" value to the "/search" value, which is being used to determine which action to execute. The "s" represents what type of query is being input (a String type) and the "apple" represents the query being input. 

---

__Part 2__

The first bug that we will be examining is from the filter method in the ListExamples file. The failure inducing input is listed below in the screenshot.

![Image](lab3-screenshot2_1.png)

The symptoms were that the two items in the array were in the reverse order, as seen in the screenshot below.

![Image](lab3-screenshot2_2.png)

The bug was that when inputting the filtered Strings into a new array, the method used was the add(0, s) method instead of the add(s) method. The original implementation meant that the strings would always be added into the front of the array instead of the back. While this is a completely viable implementation, it was not what we expected. 

The symptom showcased this clearly because in order to showcase an array in the reverse order of the expected array, we would need to add the strings to the beginning of the array.

The second bug we will be examining is the reverseInPlace method from the ArrayExamples class. The failure inducing input is shown below.

![Image](lab3-screenshot2_3.png)

The symptoms (seen in the screenshot below) showed that the final element of the actual array differed from the expected array. 

![Image](lab3-screenshot2_2.png)

The bug that caused this was that while replacing elements in the original array, the elements in the later half of the array would take from the modified array instead of the original array. The fix would come in the form of reversing the array, using a loop to import those items into a separate array within the method, then using another loop to import the items from the new array back into the original.

The example from the symptom showcased this clearly. The actual array returned { 5, 4, 5 } instead of { 5, 4, 3 }. The final element was the only one that differed. This means that the first two elements were imported correctly and the last element took the 5 from the already modified array to import into the final index.
