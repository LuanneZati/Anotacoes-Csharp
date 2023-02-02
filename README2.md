## Curso C# Udemy parte 2

### **1. Modificadores de acesso**

```cs
internal - Can only be accessed by the assembly 
private - Can only be accessed by the same class
public - Free access
```

Obs: Private class can only be constructed inside another class!

``static - It can be used in attribute, property, method, struct, class``

When you have a static modifier, the attribute belongs to the class, so you can only access it without an object.
When you don't have a static modifier, you need to create an object to access the attribute.

```cs
public class Person
{
    public static string name;
}
public class Person2
{
    public string name;
}
internal class program
{
    static void Main(string[] args)
    {
        //To access attribute name of Person
        Person.name; //name class.attribute

        //To access attribute name of Person2
        Person2 obj = new Person2(); //Create an object
        obj.name; //object.attribute
    }
}
```

### **2. Interfaces**

It's a class prototype, defines methods

```cs
namespace Interfaces
{
    internal interface IVeiculo
    {
        void TurnOn();
        void TurnOff();
        void OpenDoor();
        void CloseDoor();
    }
    internal class Carro: IVeiculo
    {
        public void TurnOn()
        {
            Console.WriteLine("The car is on!");
        }
        public void TurnOff()
        {
            Console.WriteLine("The car is off!");
        }
        public void OpenDoor()
        {
            Console.WriteLine("The car door is open");
        }
        public void CloseDoor()
        {
            Console.WriteLine("The car door is closed");
        }
    }
    internal class Plane: IVeiculo
    {
        public void TurnOn()
        {
            Console.WriteLine("The plane is on!");
        }
        public void TurnOff()
        {
            Console.WriteLine("The plane is off!");
        }
        public void OpenDoor()
        {
            Console.WriteLine("The plane door is open");
        }
        public void CloseDoor()
        {
            Console.WriteLine("The plane door is closed");
        }
    }
    static void Main(string[] args)
    {
        IVeiculo myCar = new Car();
        IVeiculo myPlane = new Plane();
    }
}
```

### **3. Herança**

Allows the class to share methods, attributes and properties with other classes

```cs
class Parent
{
    public void ParentMethod()
    {
        Console.WriteLine("Parent!");
    }
}
class Child:Parent
{
    ParentMethod();
    public void ChildMethod()
    {
        Console.WriteLine("Child!");
    }
}
```

```
public - EveryBody has access;
private - Anyone has access, just the same class;
protected - can only be accessed by the child class or the class itself;
```

```cs
class Parent
{
    public ProprietyP{ get; set; }
    public void ParentMethod()
    {
        Console.WriteLine("Parent!");
    }
    public Parent(string pPropriety)
    {
        ProprietyP = "Propriety";
    }
}
class Child:Parent
{
    public ProprietyC{ get; set; }
    ParentMethod();
    public void ChildMethod()
    {
        Console.WriteLine("Child!");
    }
    public Child():base("ProprietyParent")
    {
        ProprietyC = "Propriety";
    }
}
class Program
{
    static void Main(string[] args)
        {
            Child kid = new Child();
            Console.WriteLine(kid.ProprietyP); //Output: ProprietyParent
        }
}
```
When you pass a parameter to parents, to Child you need to pass ``:base(parameter)``

### **4. Herança Abstrata**

The class with abstract modifier only can be inherited, we cannot build objects.

```cs
internal abstract class People
{
    private string name;
    public string Name { get; set; }
}
class Program
{
    static void Main(string[] args)
        {
            People Person = new People(); //It generates an error
        }
}
class Employee:People
{
    Console.WriteLine(Name);
}
```

### **5. Polimorfismo**

```cs
class Vehicle
{
    virtual public void Move()//It Needs to use virtual
    {
        Console.WriteLine("The vehicle is moving!");
    }
}
class Car:Vehicle
{
    override public void Move()//It Needs to use override
    {
        base.Move();//Output: The vehicle is moving!
        Console.WriteLine("The car is moving!");
    }
}
class Bike:Vehicle
{
    override public void Move() //It Needs to use override
    {
        Console.WriteLine("The bicycle is moving!");
    }
}
class Program
{
    static void Main(string[] args)
        {
            Car car = new Car();
            Bike bike = new Bike();

            car.Move();//Output: The car is moving!
            bike.Move();//Output: The bicycle is moving!
        }
}
```

### **6. Upcasting e Downcasting**

Upcasting: converting an object from child class to parent class  
Downcasting: converting an object from parent class to child class 

```cs
//Upcasting
static void Main(string[] args)
    {
        Employee employee = new Employee();
        Person person = employee;

        person.Method();//Print the child method
    }
//Downcasting
static void Main(string[] args)
    {
        Employee employee = new Employee();
        Person person = employee;
        Employee employee2 = (Person)person;

        employee2.Method();//Print the parent method
    }
```

### **7. Serialização e deserialização**

```cs
...It's not ready yet
```

### **8. Eventos**

Way to exchange informations between objects.  
3 steps:  
    1. Create a delegate  
    2. Create a public event  
    3. Create a method inside the class
