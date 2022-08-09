# User Input
User input for [[JAVA]] programming. We create the object scanner, but irst we need to import it
```java
import java.util.Scanner;
```

Then instantiate
```java
Scanner storeData = new Scanner(System.in);
System.out.print("Input Text: ");
String userInput = storeData.nextLine();
System.out.println("User Input is " + userInput);
```
![[Pasted image 20220711095549.png]]