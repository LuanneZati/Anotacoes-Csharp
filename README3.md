## Curso C# Udemy parte 3

### **1. DLLs**

They're as code library, contains classes, methods and other data.
Allows code reuse and they are loaded by programs at runtime.  

Loading DLL before execution 
```cs
file.dll
namespace MyFirstDLL
{
    public class Math
    {
        public static double Mum(double a, double b)
        {
            return a + b;
        }
        public static double Mult(double a, double b)
        {
            return a + b;
        }
    }
}
```
```cs
file.cs

using MyFirstDLL;
namespace LoadDLL
{
    public class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine(Math.Sum(12, 2));//Output: 14
            Console.WriteLine(Math.Mult(12, 2));//Output: 24
        }
    }
}
```

Loading DLL dynamic, while program execution

```cs
file.cs

using System.Refletion; 
namespace LoadDLL
{
    public class Program
    {
        static void Main(string[] args)
        {
            Assembly myDLL = Assembly.LoadFile(@"./path");
            Type MathClass = myDLL.GetType("MyFirstDLL.Math");
            dynamic Mathinstance = Activator.CreateInstance(MathClass);
            var SumMethod = MathClass.GetMethod("Sum");
            double result = SumMethod.Invoke(MathInstance, new object[]{10, 20}); 
            Console.WriteLine(result);//Output: 30
        }
    }
}
```
...Using a native DLL

- What is a native DLL?  
It's a DLL developed in C or C++. The codes are executed by processador, that is, there isn't interpreter reading 

```cs
file.cs

using System.Runtime.InteropServices;
namespace NativeDLL
{
    internal class NativeDLL
    {
        [DllImport(@"./path", CallingConvention = CallingConvention.Cdecl)]
        public static extern double Sum(double a, double b);
        [DllImport(@"./path", CallingConvention = CallingConvention.Cdecl)]
        public static extern double Mult(double a, double b);
    }
    public class Program
    {
        static void Main(string[] args)
        {
            double result = NativeDLL.Sum(10, 20);
            double result = NativeDLL.Mult(10, 20);
            Console.WriteLine(result);//Output: 30
        }
    }
}
```

### **2. Programação paralela e assíncrona**

```cs
using System.Threading;
namespace ParallelProgram
{
    public class Program
    {
        static Thread t1;
        static Thread t2;
        static bool finalize;

        static void MyThread()
        {
            while(finalize == false)
            {
                Consolw.WriteLine("THREAD1 - Passed 1 second..");
                Thread.sleep(1000);
            }
        }

        static void MyThread2()
        {
            while(finalize == false)
            {
                Consolw.WriteLine("THREAD2 - Passed 1 second..");
                Thread.sleep(1000);
            }
        }

        static void Main(string[] args)
        {
            finalize = false;
            t1 = new Thread(new ThreadStart(MyThread));
            t2 = new Thread(new ThreadStart(MyThread2));
            //t1.Priority = ThreadPriority.Parameter

            t1.start();
            t2.start();

            Console.ReadKey();
            finalize = true;
            //t1.Abort(); //Abort
            //t2.Abort(); //Abort
        }
    }
}
```

### **3. Threads 2**

4 ways to create threads:

```cs
Threads with input parameters

using System.Threading;
namespace ParallelProgram
{
    public class Program
    {
        public static void MyThread(object x)
        {
            do
            {
                Console.WriteLine("THREAD1 - Passed 1 second..");
                Console.WriteLine((int)x++);
                Thread.sleep(1000);
            } while(x < 20)
        }
        static void Main(string[] args)
        {
            Thread t = new Thread(new ParameterizedThreadStart(MyThread));
            t.start(10);

            Console.ReadKey();
        }
    }
}
```
```cs
using System.Threading;
namespace ParallelProgram
{
    internal class ThreadParameter
    {
        public int counter{ get; set; }
        public string name{ get; set; }

        public ThreadParameter(int counter, string name)
        {
            counter = this.counter;
            Name = this.name;
        }
    }
    public class Program
    {
        public static void MyThread(object ThreadParameter)
        {
            ThreadParameter threadParameter = (ThreadParameter)this.ThreadParameter; 
            int counter = threadParameter.counter;
            Console.WriteLine(threadParameter.name); 
            do
            {
                Console.WriteLine(counter++); 
            } while(counter < 20)
        }
        static void Main(string[] args)
        {
            Thread t = new Thread(new ParameterizedThreadStart(MyThread));
            ThreadParameter threadParameter = new ThreadParameter(12, "Maria"); 
            t.start(threadParameter);

            Console.ReadKey();
        }
    }
}
```
```cs
using System.Threading;
namespace ParallelProgram
{
    public class Program
    {
        public static void MyThread(int x, string name)
        {
            Console.WriteLine(name);
            do
            {
                Console.WriteLine("THREAD1 - Passed 1 second..");
                Console.WriteLine((int)x++);
                Thread.sleep(1000);
            } while(x < 20)
        }
        static void Main(string[] args)
        {
            Thread t = new Thread(()=> MyThread(20, "Lua"));
            t.start();

            Console.ReadKey();
        }
    }
}
```
```cs
using System.Threading;
namespace ParallelProgram
{
    public class Program
    {
        static void Main(string[] args)
        {
            int x = 10;
            string name = "Laura";
            Thread t = new Thread(()=> 
            {
                Console.WriteLine(name);
                do
                {
                    Console.WriteLine("THREAD1 - Passed 1 second..");
                    Console.WriteLine((int)x++);
                    Thread.sleep(1000);
                } while(x < 20)
            }
            );
            t.start();

            Console.ReadKey();
        }
    }
}
```

### **4. Tasks**

```cs
namespace Tasks
{
    public class Program
    {
        static void PrintMessage(int x)
        {
            for(int i = x; i < 10; i++)
            {
                Console.WriteLine(i);
                Thread.Sleep(500);
            }
        }
        static void Main(string[] args)
        {
            Task task = Task.Run(()==> PrintMessage(5));
            Console.ReadKey();
        }
    }
}
```
```cs
namespace Tasks
{
    public class Program
    {
        static int PrintMessage(int x)
        {
            for(int i = x; i < 10; i++)
            {
                Console.WriteLine(i);
                Thread.Sleep(500);
            }
            return 10;
        }
        static void Main(string[] args)
        {
            int resultTask = 0;
            Task task = Task.Run(()==> resultTask = PrintMessage(5));
            if(PrintMessage.Wait(10000) == false) //Wait for task to finish
            {
                Console.WriteLine("Task still isn't finished..");    
            }
            else
            {
                Console.WriteLine(resultTask);
            }

            Console.ReadKey();
        }
    }
}
```  

### **5. System Timers**

```cs
using System.Timers;

namespace SystemTimers
{
    internal class Program
    {
        static void TimerTick(object sender, EventArgs e)
        {
            Console.WriteLine(DateTime.Now.ToString("hh:mm:ss"));
        }
        static void Main(string[] args)
        {
            //Creating timer
            Timer timer = new Timer(1000);
            timer.autoReset = true;
            timer.Elapsed += TimerTick;

            timer.start();

            Console.WriteLine("Press any key..");
            Console.ReadKey();

            timer.stop();
        }
    }
}
```

### **6. System Threading Timer**

```cs
using System.Threading;

namespace SystemTimers
{
    internal class Program
    {
        static void TimerTick(object state)
        {
            Console.WriteLine(DateTime.Now.ToString("hh:mm:ss"));
        }
        static void Main(string[] args)
        {
            //Creating timer
            TimerCallback timer = new TimerCallback(TimerTick);
            Timer myTimer = new Timer(timer, null, 0, 1000); //(callback, function parameter object, lag time, time to execute )

            Console.WriteLine("Press any key..");
            Console.ReadKey();

            myTimer.Dispose();
        }
    }
}