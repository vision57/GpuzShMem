Remark of this fork:

- Try to protect shared memory access by a cas lock on field `busy`, and upgrade project to vs2019.
- I'm not professional windows developer, the binary release is tested on my developing environment(Win10/vs2019/dotnet sdk) only.

--------------

This repository contains two visual studio 2010 projects, one that's written in C++ and used to create a .dll and the other one to show how you can access the shared memory via the .dll in C#. Usually including the .dll into your project (such as done in the demo project) will be sufficient, but if that doesn't work, you might try to adjust/compile the .dll project by yourself. I've also compiled a x64 version of the .dll, but normally the 32 bit version should work also on all 64 bit OS.

Here is a short snippet from the demo project, showing how the shared memory can be accessed:

Code:

```csharp
GpuzWrapper gpuz = new GpuzWrapper();
gpuz.Open();
Console.WriteLine(gpuz.DataKey(0) + ": " + gpuz.DataValue(0));
Console.WriteLine(gpuz.SensorName(0) + ": " + gpuz.SensorValue(0) + " " + gpuz.SensorUnit(0));
gpuz.Close();
```

Output:

```
DirectXSupport: 11.0
GPU Core Clock: 732,1149 MHz
```

The C# code is pretty straight forward. Please don't mind that I might have not used some fancy C# stuff that would have made the GpuzWrapper more convenient, but actually I'm a Java developer that programmed the whole thing 4 years ago..

Feel free to enjoy the demo and ask if something is unclear.

PS: You might have to update the location of the GpuzShMem.dll file in the GpuzDemo project. I think visual studio uses the absolute path. -.-
