# Midjourney-Input-Functions
A 512-bit and 256-bit version of a Python program that deterministically converts cryptographic public keys and hints to a sentence string for AI image generation. This project was motivated for the purpose of producing NFT art for _Pauli Group's_ post-quantum cryptographic challenges. 

# Initialization
The program begins by inputting Python's built-in Math module, as well as the contents of the separate, list-containing file. This IPYNB notebook houses extensive lists, ranging from two bits to twenty bits in length. Each list corresponds to a particular genre of terms; that is, adjectives, nouns, adverbs, styles, emotions, and more. Some lists are entirely numerical, which are later referenced as image weightings, seed values, and stylize values. In the main program, a master list containing the nested lists is generated in the _general_ framework of which the final sentence will be outputted. This means repetitions of particular lists are included. Note that the cummulative bit usage of said nested lists sums to either 512 or 256 for the 512-bit version and 256-bit version, respectively. A secondary master list is created identical to the first, however, each element holds a string of the title of each nested list in the former. This serves a purpose for iteration only.

# Binary Generation
