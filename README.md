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
       - Singleton pattern specifies that only single instance of a class should exist with a global point of access. In Kotlin we can create singleton class using ```object```.
       
       - eg:
       ```
        class Singleton 
        { 
            private static Singleton obj; 

            // private constructor to force use of 
            // getInstance() to create Singleton object 
            private Singleton() {} 

            public static Singleton getInstance() 
            { 
                if (obj==null) 
                    obj = new Singleton(); 
                return obj; 
            } 
        } 
       ```
     - **Dependency Injection**
       - Dependency injection pattern provides all the objects needed by a class to instantiate the objects without using any constructor or customizing an object. 
       - Dagger2 is the most common library used to provide dependency injection in Android.
  
  2. **Structural** : Focuses on how the classes inherit from each other and how they are composed from other classes.
     - **Composite**
       - Composite pattern is a partitioning design pattern and describes group of objects that is treated as single instance of same type of object.
       - The intent of composite is to compose objects into a tree structures which represent part or whole heirarchies.  
       - eg: In an organization, It have general managers and under general managers, there can be managers and under managers there can be developers. Now you can set a tree structure and ask each node to perform common operation like getSalary(). Composite design pattern treats each node in two ways:
         1) Composite – Composite means it can have other objects below it.
         2) leaf – leaf means it has no objects below it.
     - **Facade**
       - Facade pattern describes a higher level interface that makes sub-systems easier to use. It hides the complexity os the sub system from the client.
       - Retrofit library helps us to create Facade pattern into our applications.
       - We create an interface to provide API data to our client classes as shown below.
         ```
         interface ShopsApi {
            @GET("shops")
            fun listShops(): Call<List<Shop>>
         }
         ```
       - The client simply needs to call listShops() to receive a list of Shop objects in the callback. 
       - We can o all the customizations underneath without affecting the client. We can add a customized JSon Deserializer in our retrofit object and our Activity will have no clue about underlying process. 
       - The less each object knows about what’s going on behind the scenes, the easier it will be for Future You to manage changes in the app. This pattern can be used in a lot of other contexts; Retrofit is only one mechanism among many.
     - **Adapter**
       - Adapter pattern converts the interface of a class into another interface the client wants. The adapter pattern in known as a wrapper.
       - It allows two or more incompatible obejcts to interact. 
       - It allows reusability of existing functionality. 
       - eg: A ```RecyclerView``` is same component used among all the Android apps. But we can create different ```RecyclerView.Adapter``` classes according to our need to fit into ```RecyclerView``` object. 
  
  3. **Behavioral** : Focuses on how the coordination between objects is done. The interaction between objects should be in such a way that they can easiy comunicate with each other and are not tightly coupled.
     - **Command**
       - A Command pattern lets you issue a request without knowing the receiver. You encapsulate request as an object and send it off; deciding how to complete the request is different mechanism. 
       - It separates the object that invokes the operation from the object that actually performs the operation.
       - EventBus is an Android libray that follows this pattern. 
     - **Observer**
       - The Observer Pattern defines a one to many dependency between objects so that one object changes state, all of its dependents are notified and updated automatically.
       - One to many dependency is between Subject(One) and Observer(Many).
       - The ```RxAndroid``` library in Android lets us implement Observer pattern. 
       - eg : 
         ```
         apiService.getData(someData)
          .subscribeOn(Schedulers.io())
          .observeOn(AndroidSchedulers.mainThread())
          .subscribe (/* an Observer */)
         ```
       - In short, you define Observable objects that will emit values. These values can emit all at once, as a continuous stream, or at any rate and duration.Subscriber objects will listen for these values and react to them as they arrive. For example, you can open a subscription when you make an API call, listen for the response from the server, and react accordingly.
     - **MVVM**
     - **MVP**

