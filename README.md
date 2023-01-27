## Curso C# Udemy

### **1. Capturar um caracter pressionado**

```cs
char keyPressed = Console.ReadKey(true).KeyChar; //Reading the unique key pressed 
Console.WriteLine(keyPressed);
```

### **2. Operadores lógicos entre numeros**

```cs
int num = 0b01010101; //Need to put 0b
int num2 = 0b00001010;
int neg = ~num;
int or = num | num2;
int and = num & num2;
int xor = num ^ num2;

Console.WriteLine(neg); 
//Output = 10101010
Console.WriteLine(or); 
//Output = 01011111
Console.WriteLine(and); 
//Output = 00000000
Console.WriteLine(xor); 
//Output = 01011111
```

### **3. Arredondando numeros**

```cs
double round = 3.33;
Console.WriteLine(Math.Ceiling(round)); //Para cima
Console.WriteLine(Math.Floor(round)); //Para baixo
```

### **4. DateTime**

```cs
DateTime date = new DateTime(2023,01,24);
DateTime dataTime = new DateTime(2023,01,24,13,35,50);

//Acessing
Console.WriteLine($"Year: {dataTime.Year}");
Console.WriteLine($"Month: {dataTime.Month}");
Console.WriteLine($"Day: {dataTime.Day}");
Console.WriteLine($"Hour: {dataTime.Hour}");
Console.WriteLine($"Minutes: {dataTime.Minute}");
Console.WriteLine($"Seconds: {dataTime.Second}");
Console.WriteLine($"Day of week: {dataTime.DayOfWeek}");

Console.WriteLine(dataTime.ToString()); //Full date

//Now
DateTime dhNow = DateTime.Now;
Console.WriteLine(dhNow.ToString()); //Full date

//String to DateTime
DateTime dataConvert = Convert.ToDateTime("24/01/2023 13:48:55");
Console.WriteLine(dataConvert);

//Formatting printed date and time
Console.WriteLine(dataConvert.ToString("yyyy-MM-dd HH-mm-ss"));

//Add and subtracting date .Add(date)
dataTime = dataTime.AddDays(7);
Console.WriteLine(dataTime);
dataTime = dataTime.AddDays(-7);
Console.WriteLine("Subtracting: " + dataTime);

//Time interval
dataTime = dataTime.Add(new TimeSpan(1, 55, 30));
```

### **5. Manipulação de Strings**

```cs
//Strings replacement
string adress = "Street ABC";
adress = adress.Replace("ABC", "CBA"); //change ABC to CBA

//Remoção de strings
string adress2 = "Street 123 ABC";
adress2 = adress2.Replace("ABC", ""); //change ABC to nothing
//ou
string adress2 = "Rua 123 ABC";
adress2 = adress2.Remove(8,3); //(index, how many characters remove)

//Contains
string name = "Bruna da Silva"
bool contains = name.Contains("Bruna");
//Output True if there is "Bruna" and False if there isn't

//text location
int index = name.IndexOf("na");
//Output index where's "na"

//Split string
string[] divider = {"da"};
string[] result = name.Split(divider, StringSplitOptions.None);

foreach(string word in result)
{
    Console.WriteLine(word); //output Bruna Silva
}

//Substring
string lastName = name.Substring(10, 5); //(index first letter, word length) 

//Composite formatting
string name = "Bruna {0} {1}";
Console.WriteLine(name, "da", "Silva"); //Output Bruna Da Silva
string fullName = String.Format(name, "Da", "Silva")
```

### **6. Enums**

São tipos que possuem valores numéricos associados a nomes (cada valor está ligado a um nome)

```cs
class Program
{
    enum RealNote
    {
        Note2 = 2,
        Note5 = 5,
        Note10 = 10
    }; //Obs: it cannot be float, just int. It's like JSON.
    static void Main(string[] args)
    {
        RealNote myNote = RealNote.Note10;
        Console.WriteLine(myNote + " is worth: " + Convert.ToInt32(myNote)); 
        //Output: Note10 value: 10
    }
}
```

```cs
class Program
{
    enum TestNote
    {
        Note0 = 0,
        Note1,
        Note2,
        Note3,
        Note4
    } //0 - 1 - 2 - 3 - 4... when you define a number, the subsequent accompany 
    static void Main(string[] args)
    {
        TesteNote myNote = TesteNote.Note4;
        Console.WriteLine(myNote + " is worth: " + Convert.ToInt32(myNote));// Output: Note4 value: 4 
    }
}
```

### **7. Struct**

```cs
class Program
{
    struct RegistrationData
    {
        public string Name;
        public string Adress;
        public int Age;
        public DateTime BirthDate;
    }
    static void Main(string[] args)
    {
        RegistrationData myRagistration;
        myRegistraton.Name = "John";
        myRegistraton.Adress = "Av Sp";
        myRegistraton.age = 25;
        myRegistraton.BirthDate = Convert.ToDateTime("30/05/2000");

        Console.WriteLine(myRegistraton.Name); //Output: John
    }
}
```

### **8. Listas**

```cs
class Program
{
    static void Main(string[] args)
    {
        List<string> nameList = new List<string()>;

        //Add elements
        nameList.Add("John");
        nameList.Add("Marcos");
        nameList.Add("Bruna");
        foreach(string name in nameList)
        {
            Console.WriteLine(name);//Output John Marcos Bruna
        }

        //Remove elements
        nameList.Remove("John");
        foreach(string name in nameList)
        {
            Console.WriteLine(name);//Output Marcos Bruna
        }

        //Remove in specifics positions
        nameList.RemoveAt(1);
        foreach(string name in nameList)
        {
            Console.WriteLine(name);//Output John Bruna
        }

        //Remove multiple elements
        nameList.RemoveRange(1,2);//(from which element, how many elements)
        foreach(string name in nameList)
        {
            Console.WriteLine(name);//Output John
        }

        //Getting the numbers of elements
        nameList.Count;

        //Concatenating lists
        List<string> finalList = new List<string()>;
        List<string> newList = new List<string()>;
        newList.Add("Luanne");
        newList.Add("Maria");
        newList.Add("Gustavo");
        }

        finalList = nameList.Concat(newList).ToList(); //newList + nameList 

        //Checking if your list has certain value
        bool contain = finalList.Contains("Ana");
        Console.WriteLine(contain);//Output: False

        //What position...
        int index = newList.IndexOf("Luanne");
        Console.WriteLine(index);//Output: 3

        //where..
        List<string> whereList = finalList.Where(x => x.StartsWith("M").ToList()); //Getting every names that starts with M 

        foreach(string name in whereList)
        {
            Console.WriteLine(name);//Output Marcos Maria
        }
}
```
### **9. Filas e pilhas**

```cs
//FILA
static void Main(string[] args)
{
    Queue<string> Namesfila = new Queue<string>();
    //Add elements
    Namesfila.Enqueue("Julia");
    Namesfila.Enqueue("Maria");
    Namesfila.Enqueue("João");

    //Remove elements
    Namesfila.Dequeue();//Removed Julia (FIFO)

    //Spying elements
    Namesfila.Peek();//Spying Julia
}
```
```cs
//PILHA
static void Main(string[] args)
{
    Stack<string> NamesPilha = new Stack<string>();
    //Add elements
    NamesPilha.Push("Mariana");
    NamesPilha.Push("Alana");
    NamesPilha.Push("Luana");

    //Remove elements
    NamesPilha.Pop();//Removed Luana (LIFO)
    
    //Spying elements
    NamesPilha.Peek();//Spying Luana
}
```

Obs: Have the same methods as lists.

### **10. Tratamento de excessões**

This is an event that occurs during program execution.  
For exemple: division by 0

```cs
static void Main(string[] args)
{
    Console.Write("Enter a number: ");
    int i = Convert.ToInt32(Console.ReadLine());
    //int Result = 10/i;

    try //Mandatory
    {
        int Result = 10/i;
        Console.WriteLine("Result: " + Result);
    }
    catch(DivideByZeroException e) //Mandatory
    {
        Console.WriteLine("Exception: " + e.Message);
        //Output Exception: attempt to divide by 0
    }
    finally //Optional always be executed
    {
        Console.WriteLine("Press any key to exit..");
    }

}
```

Obs: ```catch(Exception e)``` is generic treatment.

```cs
//Forcing an exception
static void Main(string[] args)
{
    try
    {
        throw new Exception("My first exception");
        //Throw will be displayed in the "e.Message" of the catch block
    }
    catch(Exception e)
    {
        Console.WriteLine("Exception" + e.Message);
    }
    finally
    {
        Console.WriteLine("Press any key to exit..");
    }
}
```

### **11. Métodos**

```cs
class Program
{
    public static double Sum(double a, double b)
    {
        double this.Result = a + b;
        return this.Result;
    }
    public static void Hello()
    {
        Console.WriteLine("Hello!");
    }
    static void Main(string[] args)
    {
        double a = 4.5;
        double b = 7.2;
        double Result = Sum(a, b);
        Console.WriteLine(this.Result);
        Hello();
    }
}
```
```ref - the input parameter CAN be modified by the method```  
```out - the input parameter MUST be modified by the method```
```cs
//Ref
class Program
{
    public static void Mult(double a, double b, ref double Result)
    {
        Result = a * b;
    }
    static void Main(string[] args)
    {
        double a = 4.5;
        double b = 7.2;
        double Res = 0;
        Mult(a, b, ref Res);
        Console.WriteLine(this.Res);
    }
}
```
```cs
//Out
class Program
{
    public static void Div(double a, double b, out double Result)
    {
        Result = a / b;
    }
    static void Main(string[] args)
    {
        double a = 4.5;
        double b = 7.2;
        double Res = 0;
        Div(a, b, out Res);
        Console.WriteLine(this.Res);
    }
}
```

### **12. Delegates**

```cs
class Program
{
    public delegate double MyFirstDelegate(double a, double b);
    public static double Sum(double a, double b)
    {
        return a + b;
    }
    public static double Mult(double a, double b)
    {
        return a * b;
    }
    public static double Div(double a, double b)
    {
        return a / b;
    }
    static void Main(string[] args)
    {
        MyFirstDelegate myOperations;
        myOperations = Sum;
        myOperations(10,20);

        myOperations += Mult;
        myOperations += Div;

        //Output: When the delegate references more than one method, 
        //it executes every Methods, but stores the value of last method
        //(exemple: Div)
    }
}
```
```cs
class Program
{
    public delegate double MyFirstDelegate(double a, double b);

    public static double Sum(double a, double b)
    {
        return a + b;
    }
    public static double Mult(double a, double b)
    {
        return a * b;
    }
    public static double Div(double a, double b)
    {
        return a / b;
    }

    public static void ExecuteOperation(MyFirstDelegate x)
    {
        x(50,20);
    }
    static void Main(string[] args)
    {
        ExecuteOperation(Mult);//Executes Mult 50 * 20.
    }
}
```

### **13. Manipulação de arquivos (FILE.IO)**

```cs
using System.IO;

class Program
{
    static void Main(string[] args)
    {
        string path = "C:\\Users\\Luanne\\Documents\\C#\\notations\\test.txt";
        string path2 =  @"C:\Users\Luanne\Documents\C#\notations\test2.txt";

        //Building a file
        FileStream myFile = File.Create(path);
        myFile.Close();

        //Verifying if exists
        bool exists = File.Exists(path); //Returns true or false

        //Delete files
        File.Delete(path);

        //Rename and move files
        File.Move(path, path2); //(path, new path/name)

        //Writing in a text file
        string content = "Hi, my name is Luanne!";
        File.WriteAllText(path, content);//(path, text content)

        //Writing a strings array
        string[] arrayContent = {"Luanne", "Gustavo", "Maria"};
        File.WriteAllLines(path, arrayContent);//(path, array)
        //Output: Luanne Gustavo Maria in test.txt

        //Reading all content in file
        string readContent = File.ReadAllText(path);

        //Reading file content and storing in an array
        string[] readContentArray = File.ReadAllLines(path);
    }
}
```

```cs
using System.IO;

class Program
{
    static void Main(string[] args)
    {
        string path = "C:\\Users\\Luanne\\Documents\\C#\\notations\\test.txt";

        //Add text to an existing file
        string text = "Text exemple";

        //Not very correct way
        string existingText = File.ReadAllText(path);
        string finalContent = existingText + text;
        File.WriteAllText(path, finalContent);

        //More correct way
        File.AppendAllText(path, text); //(path, text you want to add)
    }
}
```

### **14. Manipulando arquivos 2**

```cs
using System.IO;

class Program
{
    static void Main(string[] args)
    {
        //Building a file
        string path = "test.txt";
        FileStream FS = File.Create(path);
        FS.Close();

        //Writing
        StreamWriter SW = new StreamWriter(path);
        SW.Write("Hi ");
        SW.Write("How ");
        SW.Write("are you?");
        SW.Close();
        //Output: in a text file: Hi How are you?
        SW.WriteLine("Hi ");//skip lines

        //Reading
        StreamReader SW2 = new StreamReader(path);
        char[] buffer = new char[128];
        SW2.Read(buffer, 4, 5);//(array, from which index, amount of characters) 
        string line = SW2.ReadLine();//Read Hi How are you?
        line = SW2.ReadLine();//Read Hi
        SW2.Close();

        //Read full file
        StreamReader full = new StreamReader(path);
        string fullFile = full.ReadToEnd();//Read everything in the file
        full.Close();
    }
}
```