
import time
​
def is_compounded(word, words_set, original_word):
    if word in words_set and word != original_word:
        return True
    for i in range(1, len(word)):
        prefix, suffix = word[:i], word[i:]
        if prefix in words_set and is_compounded(suffix, words_set, original_word):
            return True
    return False
​
def find_longest_compounded_words(file_path):
    start_time = time.time()
​
    with open("F:\Desktop\Input_01.txt", 'r') as file:
        words = file.read().splitlines()
    words_set = set(words)
​
    longest = ""
    second_longest = ""
​
    for word in sorted(words, key=len, reverse=True):
        if is_compounded(word, words_set, word):
            if len(word) > len(longest):
                second_longest, longest = longest, word
            elif len(word) > len(second_longest):
                second_longest = word
​
    end_time = time.time()
    time_taken = (end_time - start_time) * 1000  
​
    return longest, second_longest, time_taken
​
if __name__ == "__main__":
    file_name = "Input_01.txt"
    longest, second_longest, time_taken = find_longest_compounded_words(file_name)
    print(f"File: {file_name}")
    print(f"Longest Compound Word: {longest}")
    print(f"Second Longest Compound Word: {second_longest}")
    print(f"Time taken to process file: {time_taken:.2f} milliseconds")
​
File: Input_01.txt
Longest Compound Word: ratcatdogcat
Second Longest Compound Word: catsdogcats
Time taken to process file: 1.00 milliseconds
