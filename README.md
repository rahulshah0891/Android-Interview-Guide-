# Android-Interview-Guide
A Guide with all the questions related to Android Interview.

### Design Patterns

The design patterns are divided into 3 categories:
  1. **Creational** : Focuses on how you are going to create objects.
     - **Builder** 
       - Builder pattern simplifies object creation in very clean and readable way.
       - It helps creating Model(POJO) classes with many parameters in easier and efficient way.
       - We can make some of the fields optional and some required and we dont have to maintain any order.
       - Commonly used Builder pattern in Android is ```AlertDialog.Builder()```.
       - We can create our own Builder class as shown below.
          ``` 
            public class Person {
                private String firstName;
                private String lastName;
                private int age;

                private Person(Builder builder) {
                    this.firstName = builder.firstName;
                    this.lastName = builder.lastName;
                    this.age = builder.age;
                }

                static class Builder{
                    private String firstName;
                    private String lastName;
                    private int age;

                    public Builder setFirstName(String firstName) {
                        this.firstName = firstName;
                        return this;
                    }

                    public Builder setLastName(String lastName) {
                        this.lastName = lastName;
                        return this;
                    }

                    public Builder setAge(int age) {
                        this.age = age;
                        return this;
                    }

                    public Person create(){
                        return new Person(this);
                    }
                }
            }

          ```
          After that we can use it as shown below.
          ``` 
          Person person = new Person.Builder()
                            .setFirstName("John")
                            .setLastName("Wick")
                            .setAge(42)
                            .create();
          ```                  
     - **Singleton**
     - **Factory**
     - **Dependency Injection**
  
  2. **Structural** : Focuses on how the classes inherit from each other and how they are composed from other classes.
     - **Composite**
     - **Facade**
     - **Adapter**
  
  3. **Behavioral** : Focuses on how the coordination between objects is done. The interaction between objects should be in such a way that they can easiy comunicate with each other and are not tightly coupled.
     - **Command**
     - **Observer**
     - **MVVM**
     - **MVP**

