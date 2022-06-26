using System;
using System.Diagnostics;
using System.Threading;

namespace TaskbarTextStuckFix
{
    class Program
    {
        public static void Main(string[] args)
        {
            OperatingSystem os = Environment.OSVersion;
            if(os.Platform == PlatformID.Win32NT)
            {
                Console.WriteLine("Compatible OS.");
                Thread.Sleep(350);

                Process[] processes = Process.GetProcessesByName("Explorer");
                foreach (Process process in processes)
                {
                    RestartProcess(process, "Explorer");
                }
            }
            else
            {
                Console.WriteLine("Not compatible OS. Win32S, Win32Windows, WinCE not supported.");
            }
        }

        public static void RestartProcess(Process process, string processName)
        {
            try
            {
                process.Kill();
                Process newProcess = new Process();
                newProcess.StartInfo.FileName = processName;
                newProcess.Start();
            }
            catch(Exception ex)
            {
                Console.WriteLine($"{ex.Message}, restart pc? Y/N");
                string answer = Console.ReadLine();
                if(answer == "Y" || answer == "y")
                {
                    try
                    {
                        Process.Start("ShutDown", "/r"); //Restart
                    }
                    catch (Exception exc)
                    {
                        Console.WriteLine(exc.Message);
                    }
                }
            }
        }
    }
}
