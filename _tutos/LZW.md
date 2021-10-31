---
title: The LZW Compression
layout: page
# permalink: /programs/
---

*Author: Alban Fichet <alban.fichet@gmx.fr>*  
*License: BSD 3-Clause License https://opensource.org/licenses/BSD-3-Clause*  
*Last modified: Nov. 1st 2021*  
*This code is for educational purpose, not meant to be efficient or clever. Notice each function outputs the expanded dictionary which is unnecessary but practical for educative purpose.*


## Introduction

The GIF compression scheme uses LZW algorithm, the Lempel-Ziv-Welch Compression (LZW). It is an improvement on the LZ78 algorithm from Abraham Lempel and Jacob Ziv created by Terry Welch. It was patented by Unisys, the patent is now expired.

This compression scheme works with a dictionary built while reading the stream. The initial dictionary has to be populated with all possible single element values (e.g., all ASCII characters). The algorithm works by iteratively increasing the size of a window containing successive characters and add those longer strings to the dictionary. This lengthier sequence resets each time an entry is added to the dictionary.

The next time the same sequence is encountered, the compressed stream is populated with the index in the dictionary where the sequence was added.

This allows to decompress the stream without knowing the constructed dictionary. Only the initial dictionary containing all possible single words values has to be in common.

## Compression

To compress a stream, first, a dictionary of all possible single elements (characters in case of a text stream) has to be provided. Then, for each element of the stream to compress, a coding window is expended with a new character from the stream.
- If the elements in the window is in the dictionary, the window is enlarged with the new element.  
- If the elements in the window is **not** in the dictionary, 
  - the code for the previous window is appended to the compressed stream (it is in the dictionary, it was checked in the previous iteration)
  - the string of elements in the current window is added to the dictionary
  - the window resets


```python
def compress_lzw(phrase, dictionary):
    accumulator = ''
    # The initial dictionary shall be populated with every possible single element values
    # we assume this is the case
    out_dict = dictionary.copy()
    compressed = []
    
    for current_char in phrase:
        # Expand the phrase
        word = accumulator + current_char
        
        # Is the phrase is already in the dictionary?
        if word in out_dict:
            # The phrase is in the dictionary
            # we can enlarge the window
            accumulator = word
        else:
            # The phrase is not in the dictionary!
            # 1. Append the previous code to the compressed data
            compressed.append(out_dict.index(accumulator))
            # 2. Add the phrase to the dictionary
            out_dict.append(word)
            # 3. Reset sliding window
            accumulator = current_char
    
    # Append the last character to the compressed data
    compressed.append(out_dict.index(accumulator))
    
    return compressed, out_dict
```

## Decompression

To decompress a LZW stream, you only need the compressed stream and the initial dictionary used to compress the stream i.e., the dictionary containing all possible single elements.

When reading a code from the compressed stream, the corresponding value from the dictionary is issued in the decompressed stream. Then, the algorithm checks if the previous window expanded with the current decoded element exists in the dictionary.
- If it is **not** in the dictionary, it is added to it and the window reset to contain only the current decoded string
- Otherwise, the window is extended

Using this method, the dictionary is populated while decoding the string.


```python
def decompress_lzw(compressed, dictionary):
    accumulator = ''
    out_dict = dictionary.copy()
    decompressed = []
    accumulator = ''
    
    for current_code in compressed:
        # We issue the dictionary value for the read code
        current_char = out_dict[current_code]
        decompressed.append(current_char)
        
        # Check if the next larger word combination is in the dictionary
        word = accumulator + current_char[0]
        
        if not word in out_dict:
            # It isn't, add it to the dictionary
            out_dict.append(word)
            # Reset the accumulator with the current phrase
            accumulator = current_char
        else:
            # It is, we can look for a longer combination
            accumulator = word
            
    return ''.join(decompressed), out_dict
```

## Example

### Simple example

We set an initial dictionary containing lower case characters and space. This will be all possible values that can be used in the phrase to compress:


```python
init_dictionary = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z', ' ']
```

Now, we can compress our phrase using only the set of characters in the initial dictionary:


```python
phrase = 'this is a sample text to see how the lzw compression algorithm works'
compressed, dict_compress = compress_lzw(phrase, init_dictionary)
```

The built dictionary is larger than the initial dictionary containing sequence of characters founds in the phrase:


```python
print(dict_compress)
```

    ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z', ' ', 'th', 'hi', 'is', 's ', ' i', 'is ', ' a', 'a ', ' s', 'sa', 'am', 'mp', 'pl', 'le', 'e ', ' t', 'te', 'ex', 'xt', 't ', ' to', 'o ', ' se', 'ee', 'e h', 'ho', 'ow', 'w ', ' th', 'he', 'e l', 'lz', 'zw', 'w c', 'co', 'om', 'mpr', 're', 'es', 'ss', 'si', 'io', 'on', 'n ', ' al', 'lg', 'go', 'or', 'ri', 'it', 'thm', 'm ', ' w', 'wo', 'ork', 'ks']


And the compressed sequence contains the codes referring indices in the built dictionary:


```python
print(compressed)
```

    [19, 7, 8, 18, 26, 29, 26, 0, 26, 18, 0, 12, 15, 11, 4, 26, 19, 4, 23, 19, 42, 14, 35, 4, 41, 7, 14, 22, 42, 7, 41, 11, 25, 54, 2, 14, 38, 17, 4, 18, 18, 8, 14, 13, 33, 11, 6, 14, 17, 8, 27, 12, 26, 22, 74, 10, 18]


We can display which element in the stream refers to the dynamically built dictionary:


```python
c_dec = [ dict_compress[p] if p < len(init_dictionary) else '<' + str(p) + '>' for p in compressed]

print(c_dec)
```

    ['t', 'h', 'i', 's', ' ', '<29>', ' ', 'a', ' ', 's', 'a', 'm', 'p', 'l', 'e', ' ', 't', 'e', 'x', 't', '<42>', 'o', '<35>', 'e', '<41>', 'h', 'o', 'w', '<42>', 'h', '<41>', 'l', 'z', '<54>', 'c', 'o', '<38>', 'r', 'e', 's', 's', 'i', 'o', 'n', '<33>', 'l', 'g', 'o', 'r', 'i', '<27>', 'm', ' ', 'w', '<74>', 'k', 's']


The size of the compressed output is lower than the original size:


```python
print('raw size: ', len(phrase), ' | compressed size: ', len(compressed))
```

    raw size:  68  | compressed size:  57


Now, we can decompress the stream, just by using the initial dictionary:


```python
decompressed, dict_decompress = decompress_lzw(compressed, init_dictionary)
```

We can confirm that the built dictionary during the decompression match the one built during compression:


```python
print(dict_decompress)
print(dict_compress == dict_decompress)
```

    ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z', ' ', 'th', 'hi', 'is', 's ', ' i', 'is ', ' a', 'a ', ' s', 'sa', 'am', 'mp', 'pl', 'le', 'e ', ' t', 'te', 'ex', 'xt', 't ', ' to', 'o ', ' se', 'ee', 'e h', 'ho', 'ow', 'w ', ' th', 'he', 'e l', 'lz', 'zw', 'w c', 'co', 'om', 'mpr', 're', 'es', 'ss', 'si', 'io', 'on', 'n ', ' al', 'lg', 'go', 'or', 'ri', 'it', 'thm', 'm ', ' w', 'wo', 'ork', 'ks']
    True


And read the decompressed data:


```python
print(phrase)
print(decompressed)

print(phrase == decompressed)
```

    this is a sample text to see how the lzw compression algorithm works
    this is a sample text to see how the lzw compression algorithm works
    True


### Example from Wikipedia

To confirm that our code works, let's take an example from Wikipedia.

First, we compress the data:


```python
init_dictionary = [ chr(i) for i in range(256) ] # Create a dictionary from all ASCII characters
phrase = 'TOBEORNOTTOBEORTOBEORNOT'
compressed, dict_compress = compress_lzw(phrase, init_dictionary)

print('compressed data: ', compressed)
print('value code data: ', ''.join([ dict_compress[p] if p < len(init_dictionary) else '<' + str(p) + '>' for p in compressed ]))
print('expanded dictionary during compression: ', dict_compress[len(init_dictionary):])
```

    compressed data:  [84, 79, 66, 69, 79, 82, 78, 79, 84, 256, 258, 260, 265, 259, 261, 263]
    value code data:  TOBEORNOT<256><258><260><265><259><261><263>
    expanded dictionary during compression:  ['TO', 'OB', 'BE', 'EO', 'OR', 'RN', 'NO', 'OT', 'TT', 'TOB', 'BEO', 'ORT', 'TOBE', 'EOR', 'RNO']


Then we decompress it:


```python
decompressed, dict_decompress = decompress_lzw(compressed, init_dictionary)

print('decompressed data: ', decompressed)
print('built dictionary during decompression: ', dict_decompress[len(init_dictionary):])
```

    decompressed data:  TOBEORNOTTOBEORTOBEORNOT
    built dictionary during decompression:  ['TO', 'OB', 'BE', 'EO', 'OR', 'RN', 'NO', 'OT', 'TT', 'TOB', 'BEO', 'ORT', 'TOBE', 'EOR', 'RNO']


Finally, we check that the streams match:


```python
print(phrase)
print(decompressed)

print(phrase == decompressed)
```

    TOBEORNOTTOBEORTOBEORNOT
    TOBEORNOTTOBEORTOBEORNOT
    True

