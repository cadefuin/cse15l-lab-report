# Lab Report 3: Bugs and Commands (Week 5)
This lab explored the process of debugging and introduced commands such as `find`, `less`, `wc`, and `grep`. 

## Part 1: Bugs
Failure-inducing input:
```
@Test 
public void testReverseInPlace() {
  int[] input2 = {1, 2, 3};
  ArrayExamples.reverseInPlace(input2);
  assertArrayEquals(new int[]{3, 2, 1}, input2);
}
```
Non-failure-inducing input:
```
@Test 
public void testReverseInPlace() {
  int[] input1 = { 3 };
  ArrayExamples.reverseInPlace(input1);
  assertArrayEquals(new int[]{ 3 }, input1);
}
```
Symptom:
![Screenshot of Symptom](cse15l-report-3-ss-1.png)
Bug before code change:
```
static void reverseInPlace(int[] arr) {
  for(int i = 0; i < arr.length; i += 1) {
    arr[i] = arr[arr.length - i - 1];
  }
}
```
Bug after code change:
```
static void reverseInPlace(int[] arr) {
  int[] newArr = new int[arr.length];
  for(int i = 0; i < arr.length; i += 1) {
      newArr[i] = arr[arr.length - i - 1];
  }
  for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArr[i];
  }
}
```

## Part 2: Researching Commands

`grep -r` "Read all files under each directory, recursively"
```
$ grep "DNA" -r technical/biomed/

technical/biomed/1471-2091-2-10.txt:          cDNA confirmed that the CD98 heavy chain is the 6B12
technical/biomed/1471-2091-2-10.txt:          Antibodies, cell lines, cDNA
technical/biomed/1471-2091-2-10.txt:          or β1 integrin subunits [ 30 32 ] . The cDNA encoding
...
```
The command prints all of the files and lines in the biomed directory that contain the pattern. This eliminates the need to use a command such as `find` to recursively search through a directory, thus saving time and complexity.
<br><br>
```
$ grep "cell" -r technical/plos/

technical/plos/journal.pbio.0020001.txt:        to the sciences will be an excellent investment by developing nations in terms of
technical/plos/journal.pbio.0020012.txt:        regulates lifespan in worms, and SIRT-1, the human enzyme that promotes cell survival
technical/plos/journal.pbio.0020012.txt:        Drosophila , which is a huge jump from a yeast cell,” says
...
```
Similarly, the command prints all of the files and lines in the plos directory that contain the pattern. This greatly simplifies the process of searching an entire directory without inputting every file, which is very useful for large directories such as biomed and plos.

---

`grep -w` "Select only those lines containing matches that form whole words."
```
$ grep -w "DNA" -r technical/biomed/

technical/biomed/1471-2091-2-11.txt:          induced genomic DNA fragmentation in this cell line at
technical/biomed/1471-2091-2-11.txt:          genomic DNA isolated from treated cells showed that TCA
technical/biomed/1471-2091-2-11.txt:          and GCDCA induced DNA laddering in CHO.asbt.35 cells
...
```
The command only prints files and lines in the biomed directory that contain the word "DNA". The first example with the biomed directory also included articles about "cDNA". However, if it is necessary to specify the search to simply "DNA", then this command option is ideal.
<br><br>
```
$ grep -w "cell" -r technical/plos/

technical/plos/journal.pbio.0020012.txt:        regulates lifespan in worms, and SIRT-1, the human enzyme that promotes cell survival
technical/plos/journal.pbio.0020012.txt:        Drosophila , which is a huge jump from a yeast cell,” says
technical/plos/journal.pbio.0020012.txt:        mouse disease models. “We think we may have tapped into a cell survival and defence
...
```
Similarly, the command only prints files and lines in the plos directory that contain the word "cell". The first example with the plos directory also included words such as "excellent", which is vastly different from "cell" and the article may not be related to cells at all. Therefore, this command option can narrow the search to relevant words.

---

`grep [OPTION] -f FILE` "Obtain patterns from FILE, one per line."
<br><br>
Using the following `pattern-file-1.txt`:
```
DNA
RNA
```

```
$ grep -w -f pattern-file-1.txt -r technical/biomed/

technical/biomed/1471-2091-2-11.txt:          induced genomic DNA fragmentation in this cell line at
technical/biomed/1471-2091-2-11.txt:          of total RNA from the selected clones (CHO.asbt) readily
technical/biomed/1471-2091-2-11.txt:          genomic DNA isolated from treated cells showed that TCA
...
```
The command prints all files and lines in the biomed directory that contain either the word "DNA" or "RNA" from the pattern file. This allows for a more general search that includes all relevant topics listed in the pattern file.
<br><br>
Using the following `pattern-file-2.txt`:
```
epidemic
plague
```

```
$ grep -w -f pattern-file-2.txt -r technical/plos/

technical/plos/journal.pbio.0020053.txt:        typhoid, and plague, and bacteriophage therapy had a brief heyday, especially in the 1920s.
technical/plos/journal.pbio.0020121.txt:        (BSE), more commonly known as mad cow disease. Nowadays, CWD is epidemic in the United
technical/plos/journal.pbio.0020121.txt:        America, and 629 were found to have tested positive for CWD. That's a small epidemic
...
```
Similarly, the command prints all files and lines in the plos directory that contain either the word "epidemic" or "plague". When provided with a larger pattern text file, the command could provide a more comprehensive search using all relevant words in the pattern file.

---

`grep -l` "Suppress normal output; instead print the name of each input file from which output would normally have been printed"
```
$ grep -l -w -f pattern-file-1.txt -r technical/biomed/

technical/biomed/1471-2091-2-11.txt
technical/biomed/1471-2091-2-13.txt
technical/biomed/1471-2091-2-5.txt
...
```
The command only prints files in the biomed directory that match the specifications. This simplifies the output into unique files that can be referenced for reading on the specified topics.
<br><br>
```
$ grep -l -w -f pattern-file-2.txt -r technical/plos/

technical/plos/journal.pbio.0020053.txt
technical/plos/journal.pbio.0020121.txt
technical/plos/journal.pbio.0020156.txt
...
```
Similarly, the command only prints files in the plos directory that match the specifications. The output can be redirected into a file or another command for further processing, such as creating a summary of the specified topics.
<br><br>
Citation: [grep(1) - Linux manual page](https://www.man7.org/linux/man-pages/man1/grep.1.html)
