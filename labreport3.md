# Lab Report 3

## Part 1

**Failure-inducing input (as JUnit test)**
```
  @Test
  public void testReversed() {
    int[] input1 = {1, 2};
    assertArrayEquals(new int[]{2, 1}, ArrayExamples.reversed(input1));
  }
```

**Success-inducing input (as JUnit test)**
```
  @Test
  public void testReversedEmpty() {
    int[] input1 = {};
    assertArrayEquals(new int[]{}, ArrayExamples.reversed(input1));
  }
```

**Symptom**
![](/labreport3_screenshots/junit_tests.png)
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
      newArray[arr.length - i - 1] = arr[i]; // this line changed
    }
    return newArray; // and this one
  }
```
The code assigns the values of `newArray` (0s) to `arr` and returns `arr`, returning an array of 0s as a result. By switching the assignment such that values of `arr` are assigned to `newArray` and returning `newArray`, values are assigned correctly and the correct reversed array is returned. 

## Part 2

### `grep` 

**Option 1:** `-c` 

The `-c` option prints the number of matching lines per file instead of the file lines (from [Linux manual](https://man7.org/linux/man-pages/man1/grep.1.html))

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

The `-n` option includes the line number for each line that matches the search pattern (from [Linux manual](https://man7.org/linux/man-pages/man1/grep.1.html))

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

The `-r` option recursively searches each file in the directory path given for the pattern given (from [Linux manual](https://man7.org/linux/man-pages/man1/grep.1.html))

```
gauri@Renjiths-MacBook-Pro ~ pwd
/Users/gauri/Desktop/CSE15L/lab_week4/docsearch/technical

gauri@Renjiths-MacBook-Pro ~ grep -r "myocardial infarction" ./biomed 
./biomed/1471-2369-3-9.txt:        patients with myocardial infarction [ 32 ] . The percentage
./biomed/1468-6708-3-10.txt:        nonfatal myocardial infarction (MI) (the primary endpoint)
./biomed/1472-6823-3-1.txt:        hyperosmolar syndrome was acute myocardial infarction
./biomed/1478-7954-1-3.txt:          myocardial infarction, coronary insufficiency, or
./biomed/1471-2350-3-1.txt:        venous thromboembolism and myocardial infarction [ 10 11 ]
./biomed/1471-2350-3-1.txt:        myocardial infarction or arterial disease, such as specific
./biomed/1471-2377-3-4.txt:        stroke, myocardial infarction, and vascular death are often
./biomed/1472-6963-3-7.txt:        AMI - acute myocardial infarction
./biomed/1475-2891-2-1.txt:          • First event of acute myocardial infarction diagnosed
./biomed/1477-7827-1-54.txt:          myocardial infarction and was not known to have any
./biomed/1472-6963-3-13.txt:        Americans experience new or recurrent myocardial infarction
./biomed/1472-6963-3-13.txt:        these events will be a first myocardial infarction. The
./biomed/1472-6963-3-13.txt:          have a family history of early myocardial infarction. We
./biomed/1472-6947-2-7.txt:          myocardial infarction. Asking providers to deliver
./biomed/cc1044.txt:        myocardial infarction, cardiac failure or arrhythmias, and
./biomed/1472-6963-1-11.txt:        discharge after myocardial infarction (Table 4) was similar
./biomed/1472-6963-1-11.txt:        myocardial infarction, [ 40 ] acute appendicitis, [ 41 ]
./biomed/1471-2369-4-1.txt:        myocardial infarction (7%), atherosclerotic heart disease
./biomed/cvm-2-6-278.txt:        with experimental myocardial infarction, these CD34 +cells
./biomed/cvm-2-4-180.txt:        myocardial infarction; PURSUIT = Platelet Glycoprotein
./biomed/cvm-2-4-180.txt:        myocardial infarction
./biomed/cvm-2-6-286.txt:        glycoprotein; MI = myocardial infarction; PAES = Parodi
./biomed/1468-6708-3-3.txt:        death, myocardial infarction, unstable angina, percutaneous
./biomed/1468-6708-3-3.txt:        myocardial infarction and randomized them to 16 weeks of
./biomed/1468-6708-3-3.txt:        than 270 mg/dL; Q-wave myocardial infarction on admission
./biomed/1468-6708-3-3.txt:        death, non-fatal myocardial infarction, resuscitated sudden
./biomed/1468-6708-3-3.txt:        myocardial infarction and resuscitated sudden cardiac death
./biomed/1468-6708-3-3.txt:        significantly affected (eg, death, myocardial infarction,
./biomed/1468-6708-3-3.txt:        Second, patients with Q-wave myocardial infarction were not
./biomed/1468-6708-3-3.txt:        with myocardial infarction. While their short-term risk
./biomed/1468-6708-3-3.txt:        with a non-Q-wave myocardial infarction, it is still much
./biomed/1468-6708-3-3.txt:        a Q-wave myocardial infarction, who are treated with
./biomed/1468-6708-3-3.txt:        unstable angina or a non-Q wave myocardial infarction. In
./biomed/1468-6708-3-3.txt:        non-fatal myocardial infarction, or rehospitalization for
./biomed/cc343.txt:        postmyocardial infarction; the hemodynamic parameters
./biomed/cc343.txt:        in the setting of an acute myocardial infarction. Although
./biomed/cvm-2-4-187.txt:        myocardial infarction; PCI = percutaneous coronary
```

Here, `grep -r` is used to find the lines with `"myocardial infarction"` in the `./biomed` directory when the working directory is `/Users/gauri/Desktop/CSE15L/lab_week4/docsearch`. The `-r` option causes every file in the `biomed` directory to be searched, which is useful because it is a quick way to find all the articles in the directory that discuss myocardial infarctions (ie. heart attacks).  

```
gauri@Renjiths-MacBook-Pro ~ pwd
/Users/gauri/Desktop/CSE15L/lab_week4/docsearch/technical

gauri@Renjiths-MacBook-Pro ~ grep -r "myocardial infarction"  
./government/Alcohol_Problems/Session4-PDF.txt:example, only 21% of survivors of myocardial infarction are treated
./plos/pmed.0020113.txt:        While for some comorbidities (such as previous acute myocardial infarction) evidence
./plos/journal.pbio.0030131.txt:        vivo implantation into the ischemic heart following myocardial infarction, suggesting a
./plos/journal.pbio.0030131.txt:        implanted into injured heart following myocardial infarction. It is possible that these
./plos/pmed.0020160.txt:          questionnaire. Prior physician-diagnosed angina, myocardial infarction, or stroke was
./plos/pmed.0020197.txt:        myocardial infarction and stroke [1–3], prompting concern for patients with established
./plos/pmed.0020140.txt:          as hypotension, myocardial infarction, or septic shock.
./plos/pmed.0020209.txt:            never be reached for any serious side effect, like myocardial infarction.” This
./biomed/1471-2369-3-9.txt:        patients with myocardial infarction [ 32 ] . The percentage
./biomed/1468-6708-3-10.txt:        nonfatal myocardial infarction (MI) (the primary endpoint)
./biomed/1472-6823-3-1.txt:        hyperosmolar syndrome was acute myocardial infarction
./biomed/1478-7954-1-3.txt:          myocardial infarction, coronary insufficiency, or
./biomed/1471-2350-3-1.txt:        venous thromboembolism and myocardial infarction [ 10 11 ]
./biomed/1471-2350-3-1.txt:        myocardial infarction or arterial disease, such as specific
./biomed/1471-2377-3-4.txt:        stroke, myocardial infarction, and vascular death are often
./biomed/1472-6963-3-7.txt:        AMI - acute myocardial infarction
./biomed/1475-2891-2-1.txt:          • First event of acute myocardial infarction diagnosed
./biomed/1477-7827-1-54.txt:          myocardial infarction and was not known to have any
./biomed/1472-6963-3-13.txt:        Americans experience new or recurrent myocardial infarction
./biomed/1472-6963-3-13.txt:        these events will be a first myocardial infarction. The
./biomed/1472-6963-3-13.txt:          have a family history of early myocardial infarction. We
./biomed/1472-6947-2-7.txt:          myocardial infarction. Asking providers to deliver
./biomed/cc1044.txt:        myocardial infarction, cardiac failure or arrhythmias, and
./biomed/1472-6963-1-11.txt:        discharge after myocardial infarction (Table 4) was similar
./biomed/1472-6963-1-11.txt:        myocardial infarction, [ 40 ] acute appendicitis, [ 41 ]
./biomed/1471-2369-4-1.txt:        myocardial infarction (7%), atherosclerotic heart disease
./biomed/cvm-2-6-278.txt:        with experimental myocardial infarction, these CD34 +cells
./biomed/cvm-2-4-180.txt:        myocardial infarction; PURSUIT = Platelet Glycoprotein
./biomed/cvm-2-4-180.txt:        myocardial infarction
./biomed/cvm-2-6-286.txt:        glycoprotein; MI = myocardial infarction; PAES = Parodi
./biomed/1468-6708-3-3.txt:        death, myocardial infarction, unstable angina, percutaneous
./biomed/1468-6708-3-3.txt:        myocardial infarction and randomized them to 16 weeks of
./biomed/1468-6708-3-3.txt:        than 270 mg/dL; Q-wave myocardial infarction on admission
./biomed/1468-6708-3-3.txt:        death, non-fatal myocardial infarction, resuscitated sudden
./biomed/1468-6708-3-3.txt:        myocardial infarction and resuscitated sudden cardiac death
./biomed/1468-6708-3-3.txt:        significantly affected (eg, death, myocardial infarction,
./biomed/1468-6708-3-3.txt:        Second, patients with Q-wave myocardial infarction were not
./biomed/1468-6708-3-3.txt:        with myocardial infarction. While their short-term risk
./biomed/1468-6708-3-3.txt:        with a non-Q-wave myocardial infarction, it is still much
./biomed/1468-6708-3-3.txt:        a Q-wave myocardial infarction, who are treated with
./biomed/1468-6708-3-3.txt:        unstable angina or a non-Q wave myocardial infarction. In
./biomed/1468-6708-3-3.txt:        non-fatal myocardial infarction, or rehospitalization for
./biomed/cc343.txt:        postmyocardial infarction; the hemodynamic parameters
./biomed/cc343.txt:        in the setting of an acute myocardial infarction. Although
./biomed/cvm-2-4-187.txt:        myocardial infarction; PCI = percutaneous coronary
```
When not provided with a directory to search through, the `grep -r` command finds the lines with `"myocardial infarction"` in  the working directory `/Users/gauri/Desktop/CSE15L/lab_week4/docsearch`. The `-r` option causes every file in the current working directory to be searched, and we know as a result that there are mentions of myocardial infarctions in files in the `government` and `plos` directories as well.  

**Option 4:** `-m [NUM]`

The `-m [NUM]` option stops reading a file after NUM matching lines are found (from [Linux manual](https://man7.org/linux/man-pages/man1/grep.1.html))

```
gauri@Renjiths-MacBook-Pro ~ pwd
/Users/gauri/Desktop/CSE15L/lab_week4/docsearch/technical

gauri@Renjiths-MacBook-Pro ~ grep -m 5 "HIV" ./plos/pmed.0010041.txt
        The devastating effects of HIV infection worldwide are reason enough for AIDS
        control HIV replication after two short treatment interruptions [1]. This report generated
        stimulated immune response to the patient's HIV infection.
        led to induction of HIV-specific proliferative responses similar to those that had been
        observed in patients with long-term, non-progressing HIV [2]. This led Rosenberg and

```

Here, `grep -m 5` prints the first 5 lines in `./plos/pmed.0010041.txt` that match `"HIV"` when the working directory is `/Users/gauri/Desktop/CSE15L/lab_week4/docsearch`. The `-m 5` option causes the `grep` command to stop reading the file after 5 lines are found, which is useful because it significantly decreases the output printed to the terminal.  

```
gauri@Renjiths-MacBook-Pro ~ pwd
/Users/gauri/Desktop/CSE15L/lab_week4/docsearch/technical

gauri@Renjiths-MacBook-Pro ~ grep -r -m 1 "myocardial infarction" 
./government/Alcohol_Problems/Session4-PDF.txt:example, only 21% of survivors of myocardial infarction are treated
./plos/pmed.0020113.txt:        While for some comorbidities (such as previous acute myocardial infarction) evidence
./plos/journal.pbio.0030131.txt:        vivo implantation into the ischemic heart following myocardial infarction, suggesting a
./plos/pmed.0020160.txt:          questionnaire. Prior physician-diagnosed angina, myocardial infarction, or stroke was
./plos/pmed.0020197.txt:        myocardial infarction and stroke [1–3], prompting concern for patients with established
./plos/pmed.0020140.txt:          as hypotension, myocardial infarction, or septic shock.
./plos/pmed.0020209.txt:            never be reached for any serious side effect, like myocardial infarction.” This
./biomed/1471-2369-3-9.txt:        patients with myocardial infarction [ 32 ] . The percentage
./biomed/1468-6708-3-10.txt:        nonfatal myocardial infarction (MI) (the primary endpoint)
./biomed/1472-6823-3-1.txt:        hyperosmolar syndrome was acute myocardial infarction
./biomed/1478-7954-1-3.txt:          myocardial infarction, coronary insufficiency, or
./biomed/1471-2350-3-1.txt:        venous thromboembolism and myocardial infarction [ 10 11 ]
./biomed/1471-2377-3-4.txt:        stroke, myocardial infarction, and vascular death are often
./biomed/1472-6963-3-7.txt:        AMI - acute myocardial infarction
./biomed/1475-2891-2-1.txt:          • First event of acute myocardial infarction diagnosed
./biomed/1477-7827-1-54.txt:          myocardial infarction and was not known to have any
./biomed/1472-6963-3-13.txt:        Americans experience new or recurrent myocardial infarction
./biomed/1472-6947-2-7.txt:          myocardial infarction. Asking providers to deliver
./biomed/cc1044.txt:        myocardial infarction, cardiac failure or arrhythmias, and
./biomed/1472-6963-1-11.txt:        discharge after myocardial infarction (Table 4) was similar
./biomed/1471-2369-4-1.txt:        myocardial infarction (7%), atherosclerotic heart disease
./biomed/cvm-2-6-278.txt:        with experimental myocardial infarction, these CD34 +cells
./biomed/cvm-2-4-180.txt:        myocardial infarction; PURSUIT = Platelet Glycoprotein
./biomed/cvm-2-6-286.txt:        glycoprotein; MI = myocardial infarction; PAES = Parodi
./biomed/1468-6708-3-3.txt:        death, myocardial infarction, unstable angina, percutaneous
./biomed/cc343.txt:        postmyocardial infarction; the hemodynamic parameters
./biomed/cvm-2-4-187.txt:        myocardial infarction; PCI = percutaneous coronary
```
Here, the first line that contains "myocardial infarction" is printed for each file that contains that pattern in the current working directory `/Users/gauri/Desktop/CSE15L/lab_week4/docsearch`. This is useful because it only prints the first line instead of printing every single line that matches the pattern from a file, which can make the output very long; however, we can still get the number of files that contain "myocardial infarction" such as some information about the context in which the term is used.
