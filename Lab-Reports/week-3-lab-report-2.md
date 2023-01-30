# CSE 15L Lab Report #2: Servers and Bugs

*Ian Venzon - Thursday 12:00 PM - B270*

# Part 1: StringServer.java

### StringServer.java code:

![Image](https://i.imgur.com/hJK6XOe.png)

### Running StringServer:

![Image](https://i.imgur.com/ifWvWAM.png)

#### Adding the first message ("Hello!"):

![Image](https://i.imgur.com/lmqGV3S.png)

The main method being called is `handleRequest(URI url)`. This method takes in one argument (an URI object created by `Server.java`) and checks to see if the url contains the path '/add-message', which also holds the user's requested string. If it does, it uses the `getQuery()` method to split the URI after the '=' and stores the split url into an array of strings called `parameters`. It then adds the user's given string (stored in `parameters[1]`) to the public string `currentString`, followed by a newline character `\n`. Since this is the first request we are making, `currentString` is empty. 

#### Result after first message:

![Image](https://i.imgur.com/ojw2Glu.png)

#### Adding the second message ("Does this thing work?"):

![Image](https://i.imgur.com/tbSwTDV.png)

The same methods are being called when we request to add another string, but the main difference is that the public String `currentString` now holds our previously requested string plus the newline character. After we request this second message, it should appear right underneath our first message on the webpage.

#### Result after second message:

![Image](https://i.imgur.com/0jr4aR2.png)

#### Adding the final message ("Looks like it does!"):

![Image](https://i.imgur.com/wK7HlGA.png)

Let's add one more message for good measure. Note that since the `Handler` class returns `currentString` no matter what url we have, we can remove the `/add=message` path from the url and we will still see all of our added messages!

#### Final Result:

![Image](https://i.imgur.com/8q57SgZ.png)

---

# Part 2: Bugs from Lab 3


---

# Part 3: Something I Learned
