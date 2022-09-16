---
aliases: [infrared sensor]
---
# HC-SR501
## DataSheet
Data sheet of this [HC-SR501](https://www.mpja.com/download/31227sc.pdf)

## Basic
![[Pasted image 20220713170258.png]]

Analyzing this, we could see that it could accept 5v as a pwoer source so we don;t need any voltage regulator for this. The output voltage also is only 3.3 v which is [[Arduino]] friendly. It also detects in a longer range as in 7 meter, maybe readius and 120 degrees. 

![[Pasted image 20220713170538.png]]

it also have 2 [[Potentiometer]] that could adjust sensitivity or the range of detection and time or the time duration of the trigger. Single trigger will make the ouput only executes once then turn low even though there is still a motion taking place, repeat trigger will output HIGH as long as there is a motion taking place. 

We could test its capabilities using this wiring
![[3.1 0500 - Infrared sensor.png.png]]


![[Pasted image 20220713173131.png]]

![[chrome-capture-2022-6-13.gif]]