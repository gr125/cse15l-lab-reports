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

### `grep` 

**Option 1:** `-c`
`-c` prints the number of matching lines per file instead of the file lines (from ![Linux manual](https://man7.org/linux/man-pages/man1/grep.1.html))

```
gauri@Renjiths-MacBook-Pro ~ pwd
/Users/gauri/Desktop/CSE15L/lab_week4/docsearch/technical

gauri@Renjiths-MacBook-Pro ~ grep -c "base pair" ./biomed/gb-2001-2-6-research0021.txt 
2
```
Here, `grep -c` is used to find the number of lines with `"base pair"` in `./biomed/gb-2001-2-6-research0021.txt` when the working directory is `/Users/gauri/Desktop/CSE15L/lab_week4/docsearch`. This is useful because the `-c` tells you how many times `"base pair"` is mentioned in this file, which can indicate how important the topic of base pairs is to the file. 

```
gauri@Renjiths-MacBook-Pro ~ pwd  
/Users/gauri/Desktop/CSE15L/lab_week4/docsearch

gauri@Renjiths-MacBook-Pro ~ grep -c "HIV" ./plos/pmed.0010041.txt 
21
```
Here, `grep -c` is used to find the number of lines with `"HIV"` in `./plos/pmed.0010041.txt` when the working directory is `/Users/gauri/Desktop/CSE15L/lab_week4/docsearch`. This is useful because the `-c` tells you how many times `"HIV"` is mentioned in this file, and since it is mentioned 21 times, we can assume that the topic of HIV is somewhat important.  

**Option 2:** `-n`
`-n` includes the line number for each line that matches the search pattern (from ![Linux manual](https://man7.org/linux/man-pages/man1/grep.1.html))

```
gauri@Renjiths-MacBook-Pro ~ pwd
/Users/gauri/Desktop/CSE15L/lab_week4/docsearch/technical

gauri@Renjiths-MacBook-Pro ~ grep -n "base pair" ./biomed/gb-2001-2-6-research0021.txt 
13:          a span of 69,034 base pairs [ 2]. Human mitochondrial DNA
15:          2 rRNAs and 22 tRNAs) over 16,569 base pairs [ 3]. All
```
Here, `grep -n` is used to find the lines with `"base pair"` in `./biomed/gb-2001-2-6-research0021.txt` when the working directory is `/Users/gauri/Desktop/CSE15L/lab_week4/docsearch`. The `-n` option causes the output to include the line number for each match, which is useful when you want to find the line with that pattern in the file itself.  

```
gauri@Renjiths-MacBook-Pro ~ pwd
/Users/gauri/Desktop/CSE15L/lab_week4/docsearch/technical

gauri@Renjiths-MacBook-Pro ~ grep -n "HIV" ./plos/pmed.0010041.txt                    
6:        The devastating effects of HIV infection worldwide are reason enough for AIDS
9:        control HIV replication after two short treatment interruptions [1]. This report generated
14:        stimulated immune response to the patient's HIV infection.
16:        led to induction of HIV-specific proliferative responses similar to those that had been
17:        observed in patients with long-term, non-progressing HIV [2]. This led Rosenberg and
18:        colleagues to ask whether HIV-specific proliferative responses were a necessary and
21:        therapy after early treatment raised hope that if HIV infection was treated early enough,
23:        of HIV replication [3]. Unfortunately, that's where the good news ends.
28:        both early treatment of HIV infection and supervised treatment interruptions (STIs) as a
33:        antiretroviral drug resistance in patients randomized to receive STIs. HIV-specific immune
39:        pre-treatment levels [5]. Other studies indicated that HIV-specific CD4+ T cells were being
42:        decreased HIV replication [7]. Despite multiple attempts, early reports of an inverse
43:        correlation between simple HIV-specific T cell responses and virologic control were not
46:        response to HIV, and not the other way around [9]. Thus, no evidence of “immune boosting”
49:        superinfected with a second strain of HIV despite excellent control of viral replication
70:        This study raises important questions in our understanding of HIV pathogenesis,
86:        Finally, is this good or bad news for HIV vaccine development? Since most current
90:        that phenotypic and functional assessments of HIV-specific T cell responses, even in
93:        Therefore, the T cell responses in the patients treated for acute HIV infection in Kaufmann
95:        determined how much this adversely affects the HIV-specific immune response, and whether an
97:        before any HIV replication (a prophylactic vaccine) might be better able
```
Here, `grep -n` is used to find the lines with `"HIV"` in `./plos/pmed.0010041.txt` when the working directory is `/Users/gauri/Desktop/CSE15L/lab_week4/docsearch`. The `-n` option causes the output to include the line number for each match, which is useful when you want to find mention of "HIV" in the file itself.  

**Option 3:** `-r`

**Option 4:** `-v`