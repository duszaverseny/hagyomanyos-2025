# Dusza Árpád Programozó Emlékverseny
*Hagyományos programozói verseny, 1. forduló, 2025. november 7-9.*

Kedves versenyzők! Ebben a GitHub repository-ban hasznos információkat találtok
a versennyel kapcsolatban.

A feladatkiírás szövegét pdf formátumban itt is megtaláljátok:

[Feladatkiírás](./Hivatalos%20feladatkiírás%20-%20Hagyományos%20verseny.pdf)

## Parancsssori paraméterek kezelése

### python

```python
import sys
from pathlib import Path

def main():
    if len(sys.argv) == 1:
        print("Használat: python script.py [--ui | <test_dir_path>]")
        sys.exit(1)

    if sys.argv[1] == "--ui":
        run_ui()
    else:
        run_automated_test(sys.argv[1])


def run_ui():
    # ...
    pass

def run_automated_test(test_dir_path):
    with open(Path(test_dir_path) / 'in.txt', 'r') as f:
        # ...
        pass

if __name__ == "__main__":
    main()
```

### c++
```cpp
#include <iostream>
#include <string>

void runUI() {
   //...
}

void runAutomatedTest(const std::string& testDirPath) {
   //...
}

int main(int argc, char* argv[]) {
    if (argc == 1) {
        std::cerr << "Használat: " << argv[0] << " [--ui | <test_dir_path>]\n";
        return 1;
    }

    const std::string param = argv[1];
    if (param == "--ui") {
        runUI();
    } else {
        runAutomatedTest(param);
    }

    return 0;
}

```


### C# Wpf

Módosítsátok az App.xaml.cs filet az alábbi minta alapján:

App.xaml.cs
```cs
using System.Configuration;
using System.Data;
using System.Diagnostics;
using System.IO;
using System.Runtime.InteropServices;
using System.Windows;

namespace WpfApp1;

public partial class App : Application
{
    protected override void OnStartup(StartupEventArgs e)
    {
        AttachConsole(-1);
        base.OnStartup(e);

        if (e.Args.Length == 0)
        {
            Console.WriteLine("Használat: WpfApp1.exe [--ui | <test_dir_path>]");
            Shutdown(1);
            return;
        }

        if (e.Args[0] == "--ui")
        {
            // Játék mód
            return;
        }

        // Teszt mód
        try
        {
            RunAutomatedTest(e.Args[0]);
        }
        catch (Exception ex)
        {
            Console.WriteLine(ex);
        }
        finally
        {
            Shutdown();
        }
    }

    private void RunAutomatedTest(string v)
    {
        // ...
    }

    [DllImport("Kernel32.dll")]
    private static extern bool AttachConsole(int processId);
}
```


### C# WinForms

Módosítsátok a Program.cs filet az alábbiak szerint:

Program.cs

```cs
using System.Runtime.InteropServices;

namespace WinFormsApp1
{
    internal static class Program
    {
        [STAThread]
        static void Main()
        {
            AttachConsole(-1);
            string[] args = Environment.GetCommandLineArgs();

            if (args.Length < 2)
            {
                Console.WriteLine("Használat: WinFormsApp1.exe [--ui | <test_dir_path>]");
                return;
            }

            if (args[1] == "--ui")
            {
                ApplicationConfiguration.Initialize();
                Application.Run(new Form1());
                return;
            }

            try
            {
                RunAutomatedTest(args[1]);
            } catch (Exception ex)
            {
                Console.WriteLine(ex);
            }
        }

        private static void RunAutomatedTest(string v)
        {
            // ...
        }

        [DllImport("Kernel32.dll")]
        private static extern bool AttachConsole(int processId);
    }
}
```
