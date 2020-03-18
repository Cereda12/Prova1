using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.IO;


namespace Forms1
{
    public struct Prodotto
    {
        public string codice;
        public string descrizione;
        public string categoria;
        public decimal prezzo;
    }

    public class MyLibrary
    {
        public static int Cerca(Prodotto[] EleP,int num, string pdc)
        {
            int x = default(int);

            int pos = -1;

            while (x < num)
            {
                if (string.Compare(EleP[x].codice, pdc) == 0)
                {
                    pos = x;
                }
                x++;
            }

            return pos;
        }

       
        public static void SalvaFile(Prodotto[] EleP, int num, string PathArchivio)
        {
            int x = 0;

            StreamWriter mioFile;

            mioFile = new StreamWriter(PathArchivio);

            while (x < num)
            {
                mioFile.WriteLine(EleP[x].codice);
                mioFile.WriteLine(EleP[x].descrizione);
                mioFile.WriteLine(EleP[x].categoria);
                mioFile.WriteLine(EleP[x].prezzo.ToString());

                x++;
            }
            mioFile.Close();
        }

        public static bool LeggiFile(Prodotto[] EleP, ref int num, string PathFile)
        {

            StreamReader miofile;
            miofile = new StreamReader(PathFile);
            Prodotto nuovoprodotto = default(Prodotto);
            num = 0;

            while (miofile.EndOfStream == false)
            {
                nuovoprodotto.codice = miofile.ReadLine();
                nuovoprodotto.descrizione = miofile.ReadLine();
                nuovoprodotto.categoria = miofile.ReadLine();
                nuovoprodotto.prezzo = decimal.Parse(miofile.ReadLine());

                EleP[num] = nuovoprodotto;

                num ++;
            }

            return miofile.EndOfStream;
        }

        public static void Ordina (Prodotto[] ele, int a, int num)
        {
            int x = 0;

            Prodotto q;

            int y = 1;

            while (x < num)
            {
                while (y < num)
                {
                    if (decimal.Compare(ele[x].prezzo, ele[y].prezzo) == a)
                    {
                        q = ele[x];
                        ele[x] = ele[y];
                        ele[y] = q;
                    }
                    y++;
                }
                x++;

                y = x + 1;
            }

        }
    }
}
