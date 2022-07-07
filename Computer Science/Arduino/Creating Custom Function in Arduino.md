## Creating Custom Function
Inside our [[Arduino Programming Basic Setup]], we have 2 main functions
```cpp
void setup(){

}

void loop(){

}
```

Both of them are void so they don't return anything but we could create our own functions that will return something... or not. 
```cpp
void setup(){
	Serial.begin(9600);
	Serial.print("Addition Calculation Result");
	Serial.print(addition(1, 1));
}

void loop(){

}

int addition(int num_1, int num_2){
	return num_1 + num_2;
}
```

Here we create a function that will return an `int` but we do not do it but it it's allowed unlike [[JAVA]], for every parameters we create, we specify their supposed datatypes. 