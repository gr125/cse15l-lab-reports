# Lab Report 3

## Part 1

**Failure-inducing input (as JUnit test)**
```
@Test
public void testAverageWithoutLowestRepeats() {
  double[] input1 = {2, 2, 3, 7};
  assertEquals(4.0, ArrayExamples.averageWithoutLowest(input1), 0.001);
}
```

**Success-inducing input (as JUnit test)**
```
  @Test
  public void testReversedOneElement() {
    int[] input1 = {1};
    assertArrayEquals(new int[]{1}, ArrayExamples.reversed(input1));
  }
```

**Symptom**
![](/labreport3_screenshots/symptoms.png)

**The bug**
before:
```
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }
```
after:
```
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      newArray[arr.length - i - 1] = arr[i];
    }
    return newArray;
  }
```
The code assigns the values of `newArray` (0s) to `arr` and returns `arr`, returning an array of 0s as a result. By switching the assignment such that values of `arr` are assigned to `newArray` and returning `newArray`, values are assigned correctly and the correct reversed array is returned. 

## Part 2

