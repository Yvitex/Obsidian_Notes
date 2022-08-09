# Prototype Overlaying
It is the technique we use in order to make something appear on frame such as keyboard or other frames.

![[Pasted image 20220722090951.png]]

Make this so that when we tap in the search area, we will go to the search panel. In there, we need to overlay a keyboard image, to do this, we could connect it to the keyboard image in compacted size. This overlay should run automatically so we use the [[Prototyping|After delay]] interaciton. Set the delay with 200 milliseconds
Set it also to Open Overlay and modify the animation structure
![[Pasted image 20220722091522.png]]

Set the animation to move in
![[Pasted image 20220722091556.png]]

Then select the animation direction
![[Pasted image 20220722092332.png]]

Select close when clicking outside
![[Pasted image 20220722092419.png]]

![[chrome-capture-2022-6-22 (3).gif]]

We could also connect the overlay with the search bar so that when it closes, we could still access it by tapping through it,
![[Pasted image 20220722092607.png]]

And also we may want to connect the return icon with the previous![[Pasted image 20220722092706.png]]
![[chrome-capture-2022-6-22 (4).gif]]


