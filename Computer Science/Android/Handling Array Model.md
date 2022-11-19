---
aliases: []
---
Models are very useful in android development as it hides some implementation codes from the main activity. Specially if it is going to be used to create many instances of the object. One way to create a model is:
```java
package com.yvitex.quizapp.model;  
  
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

Full of getter and setter with constructor is the nature of a model. It is a class. The purpose of this specific code was to get questions as well as the correct answers from the [[String.xml]]. And because we have many set of questions we are going to store it inside an array like this. 
```java
private Question[] questions = new Question[]{  
        new Question(R.string.question_declaration, true),  
        new Question(R.string.question_amendments, false),  
        new Question(R.string.question_constitution, true),  
        new Question(R.string.question_independence_rights, true),  
        new Question(R.string.question_religion, true),  
        new Question(R.string.question_government_feds, false),  
        new Question(R.string.question_government, false),  
        new Question(R.string.question_government_senators, true),  
};
```

The resource is:
```xml
<resource>
    <string name="question_declaration">The (U.S.) Declaration of Independence was Adopted in 1776.</string>  
    <string name="correct_answer">That\'s correct</string>  
    <string name="wrong_answer">That\'s incorrect</string>  
    <string name="question_constitution">The Supreme law of the land is the Constitution.</string>  
    <string name="question_amendments">The (U.S.) Constitution has 26 Amendments.</string>  
    <string name="question_independence_rights">The two rights in the Declaration of Independence are:  
        \n \t <b>life</b> \n  \t <b>pursuit of happiness</b>.</string>  
    <string name="question_religion">Freedom of religion means:  
        \n \t <b>You can practice any religion, or not practice a religion</b>.</string>  
    <string name="question_government">Journalists is one branch or part of the government.</string>  
    <string name="question_government_feds">Congress does not make federal laws.</string>  
    <string name="question_government_senators">There are one hundred (100) U.S. Senators.</string>  
</resources>
```

THe application looks like this.
![[Pasted image 20221024155607.png]]

Since we already set the first question with this code.
```java
binding.questionPlaceholder.setText(questions[index].getQuestionResId());
```

The first problem would be how can we make the next button functional. We wil set a new global variable index that will track what question to set up. Also set up the binding for [[Data Binding - Binding Views]]
```java
private ActivityMainBinding binding;  
private Question[] questions = new Question[]{  
        new Question(R.string.question_declaration, true),  
        new Question(R.string.question_amendments, false),  
        new Question(R.string.question_constitution, true),  
        new Question(R.string.question_independence_rights, true),  
        new Question(R.string.question_religion, true),  
        new Question(R.string.question_government_feds, false),  
        new Question(R.string.question_government, false),  
        new Question(R.string.question_government_senators, true),  
};  
private int index = 0; // will start at index 0
```

Initialize the bindings 
```java
binding = DataBindingUtil.setContentView(this, R.layout.activity_main);
```

Use the binding to get the next button, so when we click the button we will increment the index and the show the current question
```java
binding.nextButton.setOnClickListener(view -> {  
    index++;  
    showQuestion();  
});
```

Show question is a function that will show the current question
```java
public void showQuestion(){  
    binding.questionPlaceholder.setText(questions[index].getQuestionResId());  
}
```

This will cause an OutOfBoundIndex Error. Use a modulo in the increment by the length of the array
```java
binding.nextButton.setOnClickListener(view -> {  
    index = (index + 1) % questions.length;  
    showQuestion();  
});
```

Theprev button will do a decrement that will be the same though we have some kind of check that if the index is 0, we dont have to decrement
```java
binding.prevButton.setOnClickListener(view -> {  
    if(index > 0){  
        index--;  
        showQuestion();  
    }  
});
```

For true or false button, we use a [[SnackBar Module]]. Create a function to check the correct answer
```java
public void checkAnswer(boolean userAnswer){  
    boolean correctAnswer = questions[index].isCorrectAnswer();  
    int message;  
    if(userAnswer == correctAnswer){  
        message = R.string.correct_answer;  
    }  
    else{  
        message = R.string.wrong_answer;  
    }  
    Snackbar.make(binding.imageView, message, Snackbar.LENGTH_LONG).show();  
}
```

Now create a[[Click Listener in Android]] for both of them
```java
binding.trueButton.setOnClickListener(view -> {  
    checkAnswer(true);  
});  
  
binding.falseButton.setOnClickListener(view -> {  
    checkAnswer(false);  
});
```



# Metatags
###### Related: [[Model-View-Controller Architecture]]
###### Tags: 
###### Source: 

---