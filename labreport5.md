# Lab Report 5

# Part 1

## 1: Student post on EdStem

| All values in frequency table returned by frequencyMap() are 1 |
| ---- |
| My frequencyMap() method is failing the testFrequencyMap() test, which has an input of [3, 2, 3]. When I checked the JUnit output file after running the tester, it said that my method returned a HashMap that had all the correct keys but values of 1 for each of them. In my method, I put 1 in the HashMap for a key for each instance of the key. Am I missing something? <br/><br/>Screenshot of tester output:<br/>![](/labreport5_screenshots/tester_output.png)<br/><br/>JUnit output file contents:<br/>![](/labreport5_screenshots/junit_output.png)|

## 2: TA response

| Double check the behavior of the HashMap put() method, and make sure you <br/>are using it correctly. You can also try running the tester on jdb and <br/>checking the contents of the HashMap each time you put in a value.|

## 3: Student debugging
Output of `jdb` testing: the values are added the first time but stay the same. 
```
$ javac -g -cp .:lib/* *.java
$ jdb -classpath .:lib/* org.junit.runner.JUnitCore ArrayTests
Initializing jdb ...
> stop at ArrayExamples:28
Deferring breakpoint ArrayExamples:28.
It will be set after the class is loaded.
> run
run org.junit.runner.JUnitCore ArrayTests
Set uncaught java.lang.Throwable
Set deferred uncaught java.lang.Throwable
> 
VM Started: JUnit version 4.13.2
.Set deferred breakpoint ArrayExamples:28

Breakpoint hit: "thread=main", ArrayExamples.frequencyMap(), line=28 bci=28
28          frequencies.put(num, 1);

main[1] print frequencies
 frequencies = "{}"
main[1] next
> 
Step completed: "thread=main", ArrayExamples.frequencyMap(), line=27 bci=42
27        for (int num: arr){

main[1] print frequencies
 frequencies = "{3=1}"
main[1] next
> 
Step completed: 
Breakpoint hit: "thread=main", ArrayExamples.frequencyMap(), line=28 bci=28
28          frequencies.put(num, 1);

main[1] next
> 
Step completed: "thread=main", ArrayExamples.frequencyMap(), line=27 bci=42
27        for (int num: arr){

main[1] print frequencies
 frequencies = "{2=1, 3=1}"
main[1] next
> 
Step completed: 
Breakpoint hit: "thread=main", ArrayExamples.frequencyMap(), line=28 bci=28
28          frequencies.put(num, 1);

main[1] next
> 
Step completed: "thread=main", ArrayExamples.frequencyMap(), line=27 bci=42
27        for (int num: arr){

main[1] print frequencies
 frequencies = "{2=1, 3=1}"
main[1] next
> 
Step completed: "thread=main", ArrayExamples.frequencyMap(), line=30 bci=48
30        return frequencies;

main[1] cont
> E..
Time: 81.73
There was 1 failure:
1) testFrequencyMap(ArrayTests)
java.lang.AssertionError: expected:<{2=1, 3=2}> but was:<{2=1, 3=1}>
at org.junit.Assert.fail(Assert.java:89)
at org.junit.Assert.failNotEquals(Assert.java:835)
at org.junit.Assert.assertEquals(Assert.java:120)
at org.junit.Assert.assertEquals(Assert.java:146)
at ArrayTests.testFrequencyMap(ArrayTests.java:26)

FAILURES!!!
Tests run: 3,  Failures: 1


The application exited
```
Java documentation on `put()` (highlighted part is relevant to bug)
![](/labreport5_screenshots/put_javadocumentation.png)

**Bug description:** For each integer in the list, a value of 1 is put into the HashMap corresponding to a key of that integer. However, the next time the same integer shows up in the list, a value of 1 replaces the 1 that was already in the map instead of adding to the value. 

## 4: Setup

### File & directory structure:
![](/labreport5_screenshots/file_directory_structure.png)
The current working directory should contain the `ArrayExamples.java`, `ArrayTests.java`, and `PublicTester.sh` files, and the `lib` directory that contains the `jar` files to run JUnit. The `.class` files are created as a result of running `PublicTester.sh`. The `grading-area` folder contains the `junit-output.txt` file that contains the output of `ArrayTests.java`; the directory and its contents are created after running `PublicTester.sh`.

### File contents

#### `ArrayExamples.java`
This file contains a class with methods related to arrays, adapted from the lab in week 4. The `frequencyMap()` method that I added is buggy. 
```
import java.util.HashMap;

public class ArrayExamples {

  // Changes the input array to be in reversed order
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }

  // Returns a *new* array with all the elements of the input array in reversed
  // order
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }

  // Averages all the numbers in the array except the lowest number, but leaves out the
  // lowest number when calculating. Returns 0 if there are no elements or just
  // 1 element in the array
  static HashMap<Integer, Integer> frequencyMap(int[] arr) {
    HashMap<Integer, Integer> frequencies = new HashMap<>();
    for (int num: arr){
      frequencies.put(num, 1);
    }
    return frequencies;
  }


}
```

#### `ArrayTests.java`
This file contains a class to test the `ArrayExamples` class, also adapted from the week 4 lab. I added a method to test the `frequencyMap()` method. 
```
import static org.junit.Assert.*;
import org.junit.*;
import java.util.HashMap;

public class ArrayTests {
	@Test 
	public void testReverseInPlace() {
    int[] input1 = { 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3 }, input1);
	}


  @Test
  public void testReversed() {
    int[] input1 = { };
    assertArrayEquals(new int[]{ }, ArrayExamples.reversed(input1));
  }

  @Test
  public void testFrequencyMap(){
    int[] input1 = {3, 2, 3};
    HashMap<Integer, Integer> expected = new HashMap<>();
    expected.put(3, 2);
    expected.put(2, 1);
    assertEquals(expected, ArrayExamples.frequencyMap(input1));
  }
}
```

#### `PublicTester.sh`
This bash file runs `ArrayTests.java`, writing the raw JUnit output file to the `junit-output.txt` file in the newly created `grading-area` directory, and prints the names of the failed tests and the number of tests passed to the terminal. This is a slightly different version of the autograder script my partner and I wrote in week 6's lab. 
```
CPATH='.:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar'

rm -rf grading-area

mkdir grading-area

# Draw a picture/take notes on the directory structure that's set up after
if [[ -f ArrayExamples.java ]]
then 
    echo "Compilation successful"
else 
    echo "There should be one file titled ArrayExamples.java in the directory PublicTester is in."
    exit 1
fi
# getting to this point

# Then, add here code to compile and run, and do any post-processing of the
# tests
javac -cp $CPATH *.java 
if [[ $? -ne 0 ]]
then    
    echo "Compilation error: see above."
    exit 1
fi

java -cp $CPATH org.junit.runner.JUnitCore ArrayTests > grading-area/junit-output.txt 

if [[ $(head -n 2 grading-area/junit-output.txt | tail -n 1 | grep "E") != "" ]]
then
    lastline=$(cat grading-area/junit-output.txt | tail -n 2 | head -n 1)
    tests=$(echo $lastline | awk -F '[, ]' '{print $3}')
    failures=$(echo $lastline | awk -F '[, ]' '{print $6}')
    successes=$((tests-failures))
    echo "Failed tests: "
    grep ".) test" grading-area/junit-output.txt
    echo "Number of tests passed: $successes / $tests"
else
    lastline=$(cat grading-area/junit-output.txt | tail -n 2 | head -n 1)
    numtests=$(echo $lastline | grep -o '[0-9]*' | head -1)
    echo "All tests passed"
    echo "Number of tests passed: $numtests / $numtests"
fi
```


#### `junit-output.txt`
This file contains the raw JUnit output from running `ArrayTests.java` (the output shown is before fixing the bug).
```
JUnit version 4.13.2
.E..
Time: 0.006
There was 1 failure:
1) testFrequencyMap(ArrayTests)
java.lang.AssertionError: expected:<{2=1, 3=2}> but was:<{2=1, 3=1}>
	at org.junit.Assert.fail(Assert.java:89)
	at org.junit.Assert.failNotEquals(Assert.java:835)
	at org.junit.Assert.assertEquals(Assert.java:120)
	at org.junit.Assert.assertEquals(Assert.java:146)
	at ArrayTests.testFrequencyMap(ArrayTests.java:26)

FAILURES!!!
Tests run: 3,  Failures: 1
```

### The full command line that triggers the bug
Running the tester file triggers the bug, leading to a failed test.
```
$ bash PublicTester.sh 
Compilation successful
Failed tests: 
1) testFrequencyMap(ArrayTests)
Number of tests passed: 2 / 3
```

### Fixing the bug
In `ArrayExamples.java`, replace the line ```frequencies.put(num, 1);``` with ```frequencies.put(num, frequencies.getOrDefault(num, 0)+1);```. This sets the value associated with `num` in `frequencies` with the value currently associated with `num` + 1. If `num` does not exist in `frequencies`, a value of 1 is associated with `num`. 

#### `ArrayExamples.java` (fixed)
```
import java.util.HashMap;

public class ArrayExamples {

  // Changes the input array to be in reversed order
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }

  // Returns a *new* array with all the elements of the input array in reversed
  // order
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }

  // Averages all the numbers in the array except the lowest number, but leaves out the
  // lowest number when calculating. Returns 0 if there are no elements or just
  // 1 element in the array
  static HashMap<Integer, Integer> frequencyMap(int[] arr) {
    HashMap<Integer, Integer> frequencies = new HashMap<>();
    for (int num: arr){
      frequencies.put(num, frequencies.getOrDefault(num, 0)+1); // changed line
    }
    return frequencies;
  }


}
```

# Part 2

In the second half of this quarter, I learned how to use the `jdb` debugger. Earlier, I would just debug using `print` statements and `break` statements, which is not the most effective method since I couldn't really stop the program at any point I wanted. However, in `jdb` I can set breakpoints to check the values of variables at specific points of the program using the `stop at <class id>:<line>` command and I can stop the program when it gets stuck to analyze the problem using the `suspend` command. `jdb` also works particular well when looking at tester behavior, which was something that I struggled with earlier. Learning how to use `jdb` in week 8's lab was particularly useful and I think I will use this knowledge a lot in the future . 