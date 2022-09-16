# Octal - Binary Conversion
To convert [[Octal Number System]] to [[Binary|Binary Number System]], We would group the bits together into 3 total bits per group, if it there is a vacant space, add 0 after the [[Most Significant Bit]]
![[Pasted image 20220908150500.png]]

Then we convert it individually, 
| 010 | 110 | 010 | 101 |
| --- | --- | --- | --- |
| 2   | 6   | 2   | 5    |

So the equivalent is $2625_{8}$

To revert this back: we just need to split the numbers again and reverse value it using this diagram for easier conversion

| 0   | 1   | 2   | 3   | 4   | 5   | 6   | 7   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 000 | 001 | 010 | 011 | 100 | 101 | 110 | 111    |

| 2   | 6   | 2   | 5   |
| --- | --- | --- | --- |
| 010 | 110 | 010 | 101    |
