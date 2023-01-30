# CSE 15L Lab Report #2: Servers and Bugs

*Ian Venzon - Thursday 12:00 PM - B270*

# Part 1: StringServer.java

### StringServer.java code:

![Image](https://i.imgur.com/hJK6XOe.png)

### Running StringServer:

![Image](https://i.imgur.com/ifWvWAM.png)

#### Adding the first message ("Hello!"):

![Image](https://i.imgur.com/lmqGV3S.png)

The main method being called is `handleRequest(URI url)`. This method takes in one argument (an URI object created by `Server.java`) and checks to see if the url contains the path `/add-message`, which also holds the user's requested string. If it does, it uses the `getQuery()` method to split the URI after the '=' and stores the split url into an array of strings called `parameters`. It then adds the user's given string (stored in `parameters[1]`) to the public string `currentString`, followed by a newline character `\n`. Since this is the first request we are making, `currentString` is empty. 

#### Result after first message:

![Image](https://i.imgur.com/ojw2Glu.png)

#### Adding the second message ("Does this thing work?"):

![Image](https://i.imgur.com/tbSwTDV.png)

The same methods are being called when we request to add another string, but the main difference is that the public String `currentString` now holds our previously requested string plus the newline character. After we request this second message, it should appear right underneath our first message on the webpage.

#### Result after second message:

![Image](https://i.imgur.com/0jr4aR2.png)

#### Adding the final message ("Looks like it does!"):

![Image](https://i.imgur.com/wK7HlGA.png)

Let's add one more message for good measure. Note that since the `Handler` class returns `currentString` no matter what url we have, we can remove the `/add-message` path from the url and we will still see all of our added messages!

#### Final Result:

![Image](https://i.imgur.com/8q57SgZ.png)

---

# Part 2: Bugs from Lab 3

The buggy method we will be looking for at this part of the lab report is `reverseInPlace(int arr[])` from `ArrayExamples.java`.

**Here is an example of a failure-inducing input (JUnit test #1).**

```
  @Test 
  public void testReverseInPlace() {
    int[] input2 = {5, 4, 3, 2, 1};
    ArrayExamples.reverseInPlace(input2);
    assertArrayEquals(new int[]{1, 2, 3, 4, 5}, input2);
  }
```

**Here is an example of an input that doesn't induce a failure (JUnit test #2).** 

```
  @Test 
  public void testReverseInPlace() {
    int[] input1 = {1, 1, 1};
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{1, 1, 1}, input1);
  }
```

**Here is the result of running JUnit test #1 (failure-inducing input)**

![Image](https://i.imgur.com/PxxGqeO.png)

The expected array after calling `reverseInPlace()` is `{1, 2, 3, 4, 5}` but instead we get `{1, 2, 3, 2, 1}`.

**Here is the result of running JUnit test #2 (failure-free input)**

![Image](https://i.imgur.com/mfyHxLR.png)

The expected array after calling `reverseInPlace()` is `{1, 1, 1}` and that is exactly what is returned.

*Note that this does not mean our method works correctly! As we can see in our other example input above, we have to make sure to thoroughly test our methods.*

**This is the original, buggy code for the reverseInPlace() method prior to any changes:**

```
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```
**This is the code for the reverseInPlace() method after implementing my fix**

```
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length / 2; i += 1) {
      int temp = arr[i];
      arr[i] = arr[arr.length - i - 1];
      arr[arr.length - i - 1] = temp;
    }
  }
```
These changes fix the original bug of the index at the end of the array not being changed. The for loop now only iterates for half of the array length, and a temporary variable stores the value at `arr[i]` before it is changed. This then allows for the element at `arr[arr.length - i - 1]` to be set to the value stored in the temporary variable. After the changes, the array is successfully reversed in place.

---

# Part 3: Something I Learned
