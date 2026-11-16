# EXP.NO:4  RUN A BASIC WORD COUNT MAP REDUCE PROGRAM TO UNDERSTAND MAP REDUCE PARADIGM  (PYTHON VERSION)

DATE:

AIM:
To write a basic Word Count program in Python to understand the MapReduce paradigm.

ALGORITHM:
The entire MapReduce program can be fundamentally divided into three parts:
• Mapper Phase Code
• Reducer Phase Code
• Driver Code

STEP 1: MAPPER CODE:
We create a function or class that reads each line from the input text and tokenizes it into words. Each word is assigned a value of 1.
• Input: a line of text
• Output: (word, 1)

Example:
• Dear 1, Bear 1, etc.

STEP 2 : REDUCER CODE:
We aggregate the repeated words and count how many times each word appears.
• Input: (word, [1, 1, 1, ...])
• Output: (word, total_count)

Example:
• Bear, 2; Car, 3, etc.

STEP 3: DRIVER CODE:
In the driver section, we specify the input file path and output file path. The program reads the file, processes all lines, and writes the final word counts to an output file.

PROGRAM:

```python
from collections import defaultdict


class Mapper:
    def __init__(self):
        self.output = []

    def map(self, line):
        words = line.lower().replace(',', '').replace('.', '').split()
        self.output = [(word, 1) for word in words]
        return self.output


class Reducer:
    def __init__(self):
        self.counts = defaultdict(int)

    def reduce(self, mapped_data):
        for word, value in mapped_data:
            self.counts[word] += value
        return dict(self.counts)


class WordCountDriver:
    def __init__(self, input_file, output_file):
        self.input_file = input_file
        self.output_file = output_file

    def execute(self):
        mapper = Mapper()
        reducer = Reducer()

        with open(self.input_file, 'r', encoding='utf-8') as file:
            for line in file:
                mapped_data = mapper.map(line)
                reducer.reduce(mapped_data)

        final_result = reducer.reduce([])

        with open(self.output_file, 'w', encoding='utf-8') as file:
            for word, count in sorted(final_result.items()):
                file.write(f"{word} {count}\n")

        return final_result


if __name__ == "__main__":
    input_file = "sample_input.txt"
    output_file = "sample_output.txt"

    driver = WordCountDriver(input_file, output_file)
    result = driver.execute()

    print("Word Count Result:")
    for word, count in sorted(result.items()):
        print(f"{word}: {count}")
```

EXAMPLE INPUT FILE (sample_input.txt):
```text
Hello world
Hello Python
Python is fun
world is fun
```

OUTPUT FILE (sample_output.txt):
```text
fun 2
hello 2
is 2
python 2
world 2
```

RUN THE PROGRAM:
```bash
python Experiment_4_Python.py
```

RESULT:
The program successfully counts the frequency of words in the given input file, following the same structure and logic as the MapReduce Word Count example.
