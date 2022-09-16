# Hexadecimal - Binary Conversion
To conver [[Hexadecimal Notation]] to [[Binary|Binary Number System]] and vice versa we do the following:

If we have this binary like this. we could group it by 4 bits per group
![[Pasted image 20220908151828.png]]

```ad-Danger
title: The answer above is wrong
collapse: open
Why the fuck is it so wrooooong? Check the correct answer using this [converter](https://www.rapidtables.com/convert/number/binary-to-hex.html)

```

If there is a vacant space, add 0 after the [[Most Significant Bit]]
Convert it individually, 
| 0101      | 1011      | 0101  |
| --------- | --------- | ----- |
| 4 + 1 | 8 + 2 + 1 | 4 + 1 |
| 5        | 11        | 5     |
| 5        | B         | 5     |

So the equivalent is $5B5_{10}$

We could just reverse the process in the vice versa part