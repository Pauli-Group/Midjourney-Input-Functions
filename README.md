# Midjourney Input Functions
__A 512-bit and 256-bit version of a Python program that deterministically converts cryptographic public keys and hints to a sentence string for AI image generation. This project was motivated for the purpose of producing NFT art for _Pauli Group's_ post-quantum cryptographic challenges.__

# Initialization
The program begins by inputting Python's built-in Math module, as well as the contents of the separate, list-containing file. This IPYNB notebook houses extensive lists, ranging from two bits to twenty bits in length. Each list corresponds to a particular genre of terms; that is, adjectives, nouns, adverbs, styles, emotions, and more. Some lists are entirely numerical, which are later referenced as image weightings, seed values, and stylize values. In the main program, a master list containing the nested lists is generated in the _general_ framework of which the final sentence will be outputted. This means repetitions of particular lists are included. Note that the cummulative bit usage of said nested lists sums to either 512 or 256 for the 512-bit version and 256-bit version, respectively. A secondary master list is created identical to the first, however, each element holds a string of the title of each nested list in the former. This serves an iterative purpose only.

# Binary Generation
The user is prompted to input both the public key and hint from the cryptographic challenge. '0b' is then removed from the beginning of each. The process for which the public key and hint are converted to their binary form differs slightly between the 512-bit version and 256-bit version. 

The former begins by converting the public key, first, from hexedecimal to integer form, then to binary. Once again, the '0b' is removed from the beginning of the binary public key, and only the first 257 bits are kept. The importance of this value will become apparent once the binary version of the hint is generated. A similar conversion process is performed for the hint, however, once the initial '0b' is removed, the entirety of the binary hint is maintained (255 bits). The 'result' variable then holds these appended strings, totalling to 512 bits. 

The latter, rather, begins by converting the hint from hexedecimal form to its equal integer value, then to binary. '0b' is removed from the beginning of the binary hint and the remainder is immediately appended to 'result' variable. A while loop, executed under the condition that the length of 'result' is less than the desired 256-bits, appends a bit from the beginning of the binary version of the public key to 'result'. This yields 256 bits stored in 'result'. 

The binary conversion function is called for the user-inputted public key and hint. 

# Obtaining List Values 
Within the getValues() function, the 'result' binary string is iterated through, from a designated _start_ and _end_ value. This function is best explained using a case example. In the interest of simplicity, the _start_ value will be an index of zero, and the _end_ value will be an index of the integer value yielded by calculating the logarithm base two of the length of the first nested list in the above defined master list. For this case, the _end_ value is fifteen, as the length of the list, 'stylize', is 2^15, or 32 768 bits. Note that each nested list has a bit length that can be represented by an integer power of two, ensuring that each _end_ value indeed yields and integer index. Furthermore, via iteration, the function converts the first fifteen bits to its respective integer value. The element stored at this integer index within the particular nested list, which, in this case, is the first one ('stylize'), is appended to an empty list entitled 'results'. If the nested list under analysis is a 'weights' list, this numerical value is appended to a secondary list entitled 'sum'. The importance of these values will become apparent once all function iterations are performed.

The case utilized to explain the getValues() function above exemplifies its first execution in the written program. Within a while loop - executed under the condition that the end of the master list of nested lists has not yet been reached, the _start_ value (upon each iteration) becomes the previous _end_ value, and the _end_ value becomes the logarithm base two of the length of the subsequent list within the master list. The 'decimal' variable holding each calculated integer index is, likewise, reset to zero upon each iteration. 

# Output Organization
The aforementioned 'weights' values are added together from the 'sum' list and stored in a 'test' variable. If the sum of the yielded weights is positive, the function proceeds to print values in a Midjourney-compatible fashion. If the sum of the yielded weights is negative, however, the MidJourney prompt will not proceed. In that case, all weights are flipped to be positive and values are printed in the same manner.

The 512-bit version follows the former of the below sentence structures. The 256-bit version follows the latter.

___A [detail][styles] with [colours][adjectives][adjectives][characters][adverbs][adverbs][verbs][prepositions][colours][adjectives][adjectives][objects][adverbs][verbs] and [colours][adjectives][adjectives][objects] in [emotions][locations][time period] in style of [artists] --stylize x -- seed y.___

___A [detail][styles] with [colours][adjectives][adjectives][characters][adverbs][adverbs][verbs][prepositions][colours][adjectives][adjectives][objects] in [locations] --stylize x.___
