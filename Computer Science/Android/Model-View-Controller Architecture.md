---
aliases: []
---
![[Pasted image 20221024101655.png]]

We separate the codes from this 3 layers so that the code could be scalable. When we change something on one layer, it won't affect the other. The controller is the main activity because we already know that this is the part where we connect everything together, model and views. 

Model is probably the feature or logics we could do that will handle the datas etc. For this we will generate a new package 
![[Pasted image 20221024145853.png]]

This is where we will store the java files. An example of model code could contains some [[Java Constructor]] and [[Getter and Setter in Java]].
```java
public class Question {  
    private int questionResId;  
    private boolean correctAnswer;  
  
    public Question(int questionResId, boolean correctAnswer) {  
        this.questionResId = questionResId;  
        this.correctAnswer = correctAnswer;  
    }  
      
    public Question(){  
          
    }  
  
    public int getQuestionResId() {  
        return questionResId;  
    }  
  
    public void setQuestionResId(int questionResId) {  
        this.questionResId = questionResId;  
    }  
  
    public boolean isCorrectAnswer() {  
        return correctAnswer;  
    }  
  
    public void setCorrectAnswer(boolean correctAnswer) {  
        this.correctAnswer = correctAnswer;  
    }  
}
```

Also, take note that our parameters require an Int and a boolean value. Though resource id should be a string correct? No. In [[Android Studio|xml]], everything is stored as numbers or integers so even if it look like this
```xml
<resources>  
    <string name="app_name">QuizApp</string>  
    <string name="trueValue">True</string>
</resources>
```

We still pass it to the class as numbers. That is the true nature of xml. 







# Metatags
###### Related: 
###### Tags: 
###### Source: 

---