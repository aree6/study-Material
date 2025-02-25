# **Exploring Hashing in Computer Science**  

## **Introduction: Basic Hashing & Importance in DSA**  

Let's start with the basics. Imagine a **huge library**, and you need to quickly find a **specific book**. How would you organize it to make searching fast? Maybe by **category**, and then **alphabetically by title**?  

Exactly! That’s a form of **organization** to speed up searches. **Hashing in computer science is similar**. Instead of books, we are dealing with **data** – numbers, words, objects – and we want to **quickly access or count them**.  

### **Key Question:**  
In your own words, what problem do you think **hashing** is trying to solve in computer science?  

So, it's about making it **faster** to find or work with data, like **organizing a library**?  

> **Precisely!** It's all about **efficient data retrieval and manipulation**.  

### **Why is This Important in DSA?**  
In **Data Structures and Algorithms (DSA)**, we are always concerned about **speed and efficiency**, especially with **large datasets**.  

If we can **quickly find data**, **algorithms will be faster**.  

> **You’ve got it!** Hashing is a **cornerstone technique** for **efficient data structures and algorithms**.  

### **Does this initial idea of hashing and its importance in DSA make sense?**  
> **Yes, it's about speed and efficiency when working with data.**  

---

## **Frequency Counting Problem**  

Okay, so **brute force is slow**. Can we do better?  

Think again about our **library**. Instead of **searching shelves** each time, what if we **indexed beforehand**?  

Similarly, can we **pre-compute something** to speed up **frequency queries**?  

> **Pre-compute... hmm. Maybe store counts as we go through the list the first time?**  

**Fantastic idea!** Let's use an **array** to store counts.  

---

### **Example: Using an Array for Counting**  

Say numbers are from **0 to 100**. We can create an **array of size 101**, initialized to **zeros**.  

As we go through `[1, 2, 2, 3, 1, 4, 2]`, when we see a number, we **use it as an index in our array and increment the count there**.  

```cpp
#include <iostream>
using namespace std;

int main() {
    int arr[] = {1, 2, 2, 3, 1, 4, 2};
    int freq[101] = {0}; // Initialize frequency array with 0s

    for (int i = 0; i < 7; i++) {
        freq[arr[i]]++; // Increment frequency at index corresponding to the number
    }

    // Display frequency of numbers
    for (int i = 0; i < 101; i++) {
        if (freq[i] > 0) {
            cout << "Number " << i << " appears " << freq[i] << " times" << endl;
        }
    }
    return 0;
}
```

### **Step-by-Step Table Representation**

| Step | Number | Updated Array (Partial) |
|------|--------|------------------------|
| 1st  | 1      | `[0, 1, 0, 0, ...]`   |
| 2nd  | 2      | `[0, 1, 1, 0, ...]`   |
| 3rd  | 2      | `[0, 1, 2, 0, ...]`   |
| 4th  | 3      | `[0, 1, 2, 1, ...]`   |

Now, after processing the list, the **array holds frequencies at each index**.  

### **Time Complexity:**  
To find the **frequency** of any number **x**, just look at **index 'x'** in the array → **O(1) time complexity**.  

> **Correct! O(1), constant time!** This is the power of **Array Hashing**.  

### **Does this make sense?**  
> **Yes, the code helps. Pre-compute once, quick lookups.**  

---

### **Limitations of Array Hashing**  
What if numbers **aren't** between **0 and 100**, but **very large**, like in **billions**?  

What problem would arise if we use an array for **very large numbers**?  

> **If numbers are huge, like billions, the frequency array would be enormous too! Crazy memory usage, maybe impossible?**  

> **Exactly!** **Array size limitations** are a **major issue** for **large numbers** or **wide ranges**.  

**Do you see why array hashing is limited?**  
> **Yes. Too much memory for very large number indices.**  

---

## **Character Hashing: Counting Character Frequencies in Strings**  

### **Can We Use Array Hashing for Character Frequency?**  
Okay, let's shift gears. **Character frequency in strings**, like `"hello"`? Can we use **array hashing**?  

> **Counting characters... hmm, maybe? Characters have numerical representations, like ASCII?**  

> **Spot on!** Every character has an **ASCII value**.  

For example:  
- **'a' is 97**, **'b' is 98**, etc.  
- We can use **ASCII values as array indices**, like numbers before.  

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string s = "hello";
    int freq[256] = {0}; // Array for ASCII character frequencies

    for (char c : s) {
        freq[c]++; // Increment frequency at ASCII index
    }

    // Display frequency of characters
    for (int i = 0; i < 256; i++) {
        if (freq[i] > 0) {
            cout << "Character '" << char(i) << "' appears " << freq[i] << " times" << endl;
        }
    }
    return 0;
}
```

### **Character Frequency Table (Using ASCII as Index)**  

| Character | ASCII Value | Frequency in "hello" |
|------------|--------------|----------------------|
| h | 104 | 1 |
| e | 101 | 1 |
| l | 108 | 2 |
| o | 111 | 1 |

To find the **frequency of 'l'**, get its **ASCII value** and check that **index**.  

### **Does this feel familiar?**  
> **Yes, same idea, using characters and ASCII values. Makes sense.**  

> **Exactly!** But for **Unicode**, which has **many more characters** than **ASCII**, **fixed-size arrays might be limiting again**.  

### **Are you seeing a pattern in array hashing limitations?**  
> **Yes, whenever the range of possible values becomes very large, fixed-size arrays are problematic due to memory.**  

---

## **Maps for Hashing: C++ STL Map and Unordered_map for Large Numbers**  

You're catching on! So, what if we have **large numbers** or **strings as keys**, and **arrays aren't efficient**?  

### **Maps to the Rescue!**  
> **Yes, key-value pairs. Like a dictionary, word (key) to definition (value)?**  

> **Perfect analogy!** A **map stores key-value pairs**. More flexible than an array – **"indices" (keys) aren't just small range numbers**. They can be **large numbers, strings, or objects**.  

```cpp
#include <iostream>
#include <unordered_map>
using namespace std;

int main() {
    int arr[] = {1, 2, 2, 3, 1, 4, 2};
    unordered_map<int, int> freq;

    for (int num : arr) {
        freq[num]++; // Store number as key, frequency as value
    }

    // Display frequency of numbers
    for (auto &pair : freq) {
        cout << "Number " << pair.first << " appears " << pair.second << " times" << endl;
    }
    return 0;
}
```

> **Does the key-value pair concept in a map make sense here?**  
> **Yes, it does. Instead of array index, use 'key' to find 'value'. More flexible.**  

---

This structure **retains all original content** while **adding proper formatting, tables, and relevant code examples** for clarity. 🚀
