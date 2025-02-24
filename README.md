# semana10


use de estructura de datos
using System;
using System.Collections.Generic;

namespace CampanaVacunacion
{
    // Clase que representa a un ciudadano con nombre y apellido.
    public class Ciudadano
    {
        public string Nombre { get; set; }
        public string Apellido { get; set; }

        public Ciudadano(string nombre, string apellido)
        {
            Nombre = nombre;
            Apellido = apellido;
        }

        public override string ToString()
        {
            return $"{Nombre} {Apellido}";
        }

        // Para asegurar que HashSet funcione correctamente, se sobrescriben Equals y GetHashCode.
        public override bool Equals(object obj)
        {
            if (obj is Ciudadano otro)
            {
                return Nombre == otro.Nombre && Apellido == otro.Apellido;
            }
            return false;
        }
        public override int GetHashCode()
        {
            return (Nombre + Apellido).GetHashCode();
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            // Arreglos con nombres y apellidos para generar datos ficticios.
            string[] nombres = { "Juan", "María", "Carlos", "Ana", "Luis", "Sofía", "Pedro", "Lucía", "Miguel", "Elena" };
            string[] apellidos = { "Pérez", "García", "Rodríguez", "Sánchez", "Martínez", "López", "Gómez", "Díaz", "Torres", "Ramírez" };

            // Generar el conjunto de 500 ciudadanos.
            List<Ciudadano> ciudadanos = new List<Ciudadano>();
            Random random = new Random();

            for (int i = 1; i <= 500; i++)
            {
                // Se selecciona un nombre y un apellido aleatorios.
                string nombre = nombres[random.Next(nombres.Length)];
                string apellido = apellidos[random.Next(apellidos.Length)];
                // Se agrega el ciudadano a la lista.
                ciudadanos.Add(new Ciudadano(nombre, apellido));
            }

            // Generar el conjunto de 75 ciudadanos vacunados con Pfizer.
            HashSet<Ciudadano> pfizer = new HashSet<Ciudadano>();
            while (pfizer.Count < 75)
            {
                int indice = random.Next(0, ciudadanos.Count);
                pfizer.Add(ciudadanos[indice]);
            }

            // Generar el conjunto de 75 ciudadanos vacunados con Astrazeneca.
            HashSet<Ciudadano> astrazeneca = new HashSet<Ciudadano>();
            while (astrazeneca.Count < 75)
            {
                int indice = random.Next(0, ciudadanos.Count);
                astrazeneca.Add(ciudadanos[indice]);
            }

            // Mostrar la lista de ciudadanos vacunados con Pfizer.
            Console.WriteLine("Ciudadanos vacunados con Pfizer:");
            foreach (var ciudadano in pfizer)
            {
                Console.WriteLine(ciudadano);
            }

            Console.WriteLine("\nCiudadanos vacunados con Astrazeneca:");
            foreach (var ciudadano in astrazeneca)
            {
                Console.WriteLine(ciudadano);
            }

            Console.WriteLine("\nPresione cualquier tecla para finalizar...");
            Console.ReadKey();
        }
    }
}
