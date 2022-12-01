# Verbesserung
```c#
amespace Verbesserung
{
    internal class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine();
            string[] Antwort = new string[20];
            int[] Antwort2 = new int[20];
            int Falsch = 0;
            int Resultat = 0;
            int index = 0;
            string Antwort3 = "false";
            int ri = 0;
            string Wiederholung = "No";
            int Anzahl = 20;
            string path = @"C:\Users\kochl\Desktop\IMS\BBB\Programmier Projekt\Wörter";
            do
            {
                string Englisch = @"C:\Users\kochl\Desktop\IMS\BBB\Programmier Projekt\Ordner Voci\englisch.txt";
                var englischDaten = ReadFromFile(Englisch);
                string[][] EnglischWoerter = englischDaten.Select(a => a.ToArray()).ToArray();

                string Deutsch = @"C:\Users\kochl\Desktop\IMS\BBB\Programmier Projekt\Ordner Voci\deutsch.txt";
                string[] DeutscheWörter = File.ReadAllLines(Deutsch);

                while (Antwort3 == "true")
                {
                    using (StreamReader sr = File.OpenText(path))
                    {
                        string Fehler = @"C:\Users\kochl\Desktop\IMS\BBB\Wörter.txt";
                        string[] Fehlerzahlen = File.ReadAllLines(Fehler);
                        int[] index2 = new int[20];
                        for (int m = 0; m < Fehlerzahlen.Length; m++)
                        {
                            index2[m] = Convert.ToInt32(Fehlerzahlen[m]);
                        }
                            for (int m = 0; m < 20; m++)
                            {
                                int Nummer = 0;
                                Console.Write($"Enter the English word from the German word {DeutscheWörter[index]}.");
                                Antwort[Nummer] = Console.ReadLine();

                                bool richtig = false;


                                for (int j = 0; j < EnglischWoerter[index2[m]].Length; j++)
                                {


                                    if (Antwort[Nummer] == EnglischWoerter[index2[m]][j])
                                    {
                                        richtig = true;
                                    }

                                    if (Antwort[Nummer] != EnglischWoerter[index2[m]][j])
                                    {
                                        Console.WriteLine("wrong");
                                    }

                                    if (richtig == false)
                                    {
                                        Antwort2[Nummer] = index;
                                        Falsch++;

                                    }
                                }
                            Nummer++;
                                Anzahl--;
                            }
                       
                    }
                    Antwort3 = "false";
                }

                

                Console.WriteLine("Welcome to the English Voci quiz.");

                for (int Zahl = 0; Zahl < Anzahl; Zahl++)
                {
                    var rnd = new Random();
                    index = rnd.Next(0, EnglischWoerter.Length);
                    Console.Write($"Enter the English word from the German word {DeutscheWörter[index]}.");
                    Antwort[Zahl] = Console.ReadLine();

                    bool richtig = false;


                    for (int j = 0; j < EnglischWoerter[index].Length; j++)
                    {


                        if (Antwort[Zahl] == EnglischWoerter[index][j])
                        {
                            richtig = true;
                        }

                        if (Antwort[Zahl] != EnglischWoerter[index][j])
                        {
                            Console.WriteLine("wrong");
                        }

                        if (richtig == false)
                        {
                            Antwort2[Zahl] = index;
                            Falsch++;

                        }
                    }

                }

                Console.WriteLine();

                ri = 20 - Falsch;
                Resultat = (Falsch / 20) * 100;
                Resultat = Resultat - 100;
                Console.WriteLine($"You had {ri} out of 20 correct");
                Console.WriteLine($"You got {Resultat}% right .");

                if(Falsch > 0)
                {
                    Antwort3 = "true";
                }

                for (int x = 0; x < Falsch; x++)
                {
                    Console.WriteLine();
                    Console.Write($"This is your answer:{Antwort[x]}");
                    Thread.Sleep(500);

                    Console.WriteLine();

                    for (int y = 0; y < EnglischWoerter[Antwort2[x]].Length; y++)
                    {
                        Console.Write($"This would be the right answer:{EnglischWoerter[Antwort2[x]][y]}");
                        Thread.Sleep(500);
                    }
                }


                Console.WriteLine("Do you want another round? yes/no");
                Wiederholung = Convert.ToString(Console.ReadLine());
                Thread.Sleep(10);

                                   
                if (!File.Exists(path))
                {
                                       
                    using (StreamWriter sw = File.CreateText(path))
                    {
                        for(int x = 0; x < 20; x++) 
                        { 
                        sw.WriteLine(Antwort2[x]); 
                        }
                                         
                                            
                    }
                }

            } while (Wiederholung == "yes");





        }

        static List<List<string>> ReadFromFile(string filename)
        {

            var fileData = new List<List<string>>();
            using (var sr = new StreamReader(filename))
            {
                string line;
                while ((line = sr.ReadLine()) != null)
                {
                    var fileItem = line.Split('\t').ToList();
                    fileData.Add(fileItem);
                }
                return fileData;
            }
        }
    }
}
'''
