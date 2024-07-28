# bip39-seeder

[![mail](https://img.shields.io/badge/Contact-dev%4036ip.de-blue?logo=maildotru)](mailto:dev@36ip.de)
![discord](https://img.shields.io/badge/Discord-.thirtysix-5865F2?style=flat&logo=discord)

## usecases:
1. find word by index or index by word
2. validate checksum for 12 or 24 words
3. find last word for your entropy 
4. create testdata with pi

## translate words to index or index to words

just enter words or numbers between 1 and 2048 separated by space:
```
1
```
response: 
```
query: 1
result: abandon
binary: 00000000000
```
reverse:
```
abandon
```
response: 
```
query: abandon
result: 1
binary: 00000000000
```

you can also enter multiple numbers:

```
1 3 5 7 9
```
response: 
```
query: 1 3 5 7 9
result: abandon able above absorb absurd
binary: 0000000000000000000010000000001000000000011000000001000
```
or enter multiple words:
```
abandon able above absorb absurd
```
response:
```
query: abandon able above absorb absurd
result: 1 3 5 7 9
binary: 0000000000000000000010000000001000000000011000000001000
```

<hr>

## validate checksum for 12 or 24 words

to validate the checksum just enter your words or the index for your words:

valid example
```
issue catalog crowd floor inspire insect distance emerge army diet deer bronze
```
or
```
950 288 419 716 939 937 510 582 97 494 459 230
```
response: 
```
query: issue catalog crowd floor inspire insect distance emerge army diet deer bronze
result: 950 288 419 716 939 937 510 582 97 494 459 230
binary: 011101101010010001111100110100010010110010110111010101001110101000001111111010100100010100001100000001111011010011100101000011100101
hex: 76a47cd12cb754ea0fea450c07b4e50e
sha: 52aed43b3d3182b1824520724a29ef2fff4efc9cb167867d3da188bc2d8fc3c7
checksum: 0101 is valid!
```

invalid example
```
dirt hover blush bench crack conduct artist grid keen invest enemy chaos
```
or
```
502 884 197 169 399 375 105 820 974 944 592 307
```
response: 
```
query: dirt hover blush bench crack conduct artist grid keen invest enemy chaos
result: 502 884 197 169 399 375 105 820 974 944 592 307
binary: 001111101010110111001100011000100000101010000011000111000101110110000011010000110011001101111001101011101011110100100111100100110010
hex: 3eadcc620a831c5d83433379aebd2793
sha: 5ef5a31af6bd175ecf811cd880941a5775b568b6b10b2f4da52911130ae31cc9
checksum: 0101 is invalid!
```

<hr>

## find the 12th or 24th word for your entropy

to find the last valid word for your bip39 checksum, you need an entropy by 128 bits for 12 words and 256 bits for 24 words.

every word constis of 11 bits. <br>
if you multiply 11 words by 11 bits you get 121 bits. <br>
if you multiply 23 words with 11 bits, you get 253 bits. <br>

so if you have 11 words, you need to add 7 random bits to get 128 bits.<br>
if you have 23 words, you need to add 3 bits to get 256 bits.

if you already have 11 words, enter them like:
```
hybrid inner copper evolve current gun globe address harbor junk final
```
or by the word index:
```
897 932 384 626 433 832 795 28 841 971 693
```
response:
```
query: hybrid inner copper evolve current gun globe address harbor junk final
result: 897 932 384 626 433 832 795 28 841 971 693
binary: 0111000000001110100011001011111110100111000100110110000011001111110110001101000000011011011010010000111100101001010110100
```
now take your entropy binary string and append 7 random bits, i choose "111110" for example. (if you use 23 words, you have to append only 3 random bits)

now build the checksum:
```
checksum 01110000000011101000110010111111101001110001001101100000110011111101100011010000000110110110100100001111001010010101101000111110
```
response:
```
binary: 01110000000011101000110010111111101001110001001101100000110011111101100011010000000110110110100100001111001010010101101000111110
hex: 700e8cbfa71360cfd8d01b690f295a3e
sha: 0905997d956c94ecab5f96abb0ba312666f4528103da46f6872d2b44c7a34342
valid checksum: 0000
```
then append the response checksum (in this case "0000") to the end of your entropy bits and get the words/indexes by:
```
binary 011100000000111010001100101111111010011100010011011000001100111111011000110100000001101101101001000011110010100101011010001111100000
```
response:
```
hybrid inner copper evolve current gun globe address harbor junk final lab
897 932 384 626 433 832 795 28 841 971 693 993
```
so the valid last word would be "lab" <br>
you can verify this by entering those 12 words like:
```
hybrid inner copper evolve current gun globe address harbor junk final lab
```
or
```
897 932 384 626 433 832 795 28 841 971 693 993
```
response:
```
query: hybrid inner copper evolve current gun globe address harbor junk final lab
result: 897 932 384 626 433 832 795 28 841 971 693 993
binary: 011100000000111010001100101111111010011100010011011000001100111111011000110100000001101101101001000011110010100101011010001111100000
hex: 700e8cbfa71360cfd8d01b690f295a3e
sha: 0905997d956c94ecab5f96abb0ba312666f4528103da46f6872d2b44c7a34342
checksum: 0000 is valid!
```

Yeah!

<hr>

## create testdata with pi

pi is endless, you can take random numbers from it for test purposes by enter the "pi" command
```
#pi <chunks> <chunklength> <offset>
pi 12 3 0
```
response:
```
141 592 653 589 793 238 462 643 383 279 502 884
```
if you now enter those numbers, they will translate to this response:
```
query: 141 592 653 589 793 238 462 643 383 279 502 884
result: bag enemy face end glide buffalo defy expect cool carpet dirt hover
binary: 000100011000100100111101010001100010010011000110001100000011101101001110011010101000001000101111110001000101100011111010101101110011
hex: 11893d4624c6303b4e6a822fc458fab7
sha: dd5b920b47470a19f59b6370355c269d47afe14578cc952de5041bb5915ab06f
checksum: 1101 is invalid!
```
there is also the command "pix" which will execute the response for you:
```
pix 12 3 0
```

and if you are lazy, you can just use "pixx" and it will start count the offset +1 and execute it for each keypress, until you press "esc".
```
pixx 12 3 0
```

<hr>

the code is a mess but i developed it only as a proof-of-concept and in under 6 hours. (i know, thats not a valid excuse)
