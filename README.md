# Assignment 3

Assignment 3 is a simple java program to find a frequency list of words in a given .txt file.  An input stream of song lyrics, lyrics.txt, is processed by the program to produce an output.txt file that consists of the word frequencies. 

## Installation

Copy the Assignment3.java file in the repository. 

## Usage

* Create an input file name ```lyrics.txt``` for the lyrics that you would like to analyze.
```bash
It's getting late have you seen my mates
Ma tell me when the boys get here
It's seven o'clock and I want to rock
Want to get a belly full of beer
My old man's drunker than a barrel full of monkeys
And my old lady she don't care
...
```
* Depending on the API of choice, place file in the in the necessary folder for the code to access the .txt file.
* Build and Compile the the code.  An ```output.txt``` file will be created with the word frequencies.
```bash
36: saturday
17: a
15: alright
12: nights
10: of
9: get
8: i
8: the
```


## How it works
* Assignment 3 uses the Java API to Implement a Scanner and PrintStream to input the text that needs to be analyzed and outputs the analysis
```java
Scanner in = new Scanner(new File("lyrics.txt"));
PrintStream out = new PrintStream(new File("output.txt"));
```
* An initial Hash-map is created to fill in the frequency of words that appear in the ```lyrics.txt``` file.
```java
HashMap<String, Integer> map = new HashMap<String, Integer>();
```
* The first word is retrieved from the file and assigned to a String variable.  Before being assigned, the word is formated to lower-case and any punctuation marks are removed eg. !'?...
```java
String word = in.next().toLowerCase().replaceAll
```
* The String variable "word" is then placed in the Hash-Map as the Key and its value marked as 1.  The value is 1 because this is the first occurence of the word.
```java
map.put(word, 1);
```
* A ```while``` loop is used to retrieve the rest of the words in the file.  As the words are pulled in, an ```if/else``` block is used to check whether or not a word is already in the Hash-map.  If the word exist then it's corresponding value is incremented by 1.
```java
while (in.hasNext()) {
        word = in.next().toLowerCase().replaceAll("[^a-zA-Z ]", "");
                if (map.containsKey(word)) {
                        int number = map.get(word) + 1;
                        map.put(word, number); 
                } else
                        map.put(word, 1); 
}
```
* A list object is created accepting ``Entry`` as its content, the previous hash-map is sent in as an ```entrySet```
```java
List<Map.Entry<String, Integer>> list = new LinkedList<Map.Entry<String, Integer>>(map.entrySet());
```
* ```Comparator``` class is implemented through Collections and it's compare function is written to sort the values of the correspondin keys in a descending order.
```java
Comparator<Map.Entry<String, Integer>> comparator = new Comparator<Map.Entry<String, Integer>>() {
        public int compare(Map.Entry<String, Integer> value1, Map.Entry<String, Integer> value2) {
                return (value2.getValue()).compareTo(value1.getValue());
            }
};
```
* The ```sort``` method of the ```Collection``` class is called and ```list``` and ```comparator``` is sent as it's parameters.  This enables us to sort the list in accordence to the order induced by the comparator.
```java
Collections.sort(list, comparator);
```
* The sorted list is then printed out into an output.txt file using an enhanced ```for-loop```.  For each item in the list, the loop prints out, to a text file, the ordered set of values and their key.
```java
for (Map.Entry<String, Integer> entry : list) {
        out.print(entry.getValue() + ": " + entry.getKey() + "\n");
}
```

* Values are printed out as follows:
```bash
36: saturday
17: a
15: alright
12: nights
10: of
9: get
8: i
8: the
.......
```











