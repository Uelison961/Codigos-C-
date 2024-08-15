# Codigos-C#

using System;
using System.Globalization;
using ExemploNumeros;

class Program
{
    static void Main(string[] args)
    {
        // Cria uma instância da classe Numeros
        Numeros numeros = new Numeros();

        // Solicita ao usuário a entrada de cinco números
        Console.Write("Digite o primeiro número (W): ");
        numeros.W = float.Parse(Console.ReadLine(), CultureInfo.InvariantCulture);

        Console.Write("Digite o segundo número (Waprox): ");
        numeros.Waprox = float.Parse(Console.ReadLine(), CultureInfo.InvariantCulture);

        Console.Write("Digite o terceiro número (Z): ");
        numeros.Z = float.Parse(Console.ReadLine(), CultureInfo.InvariantCulture);

        Console.Write("Digite o quarto número (Zaprox): ");
        numeros.Zaprox = float.Parse(Console.ReadLine(), CultureInfo.InvariantCulture);

        // Calcula os erros absolutos e relativos
        float eabsW = numeros.CalcularEabsW();
        float erolW = numeros.CalcularEroLW();
        float eabsZ = numeros.CalcularEabsZ();
        float erolZ = numeros.CalcularEroLZ();
        float somaErros = numeros.SomaDosErrosRelativos();

        // Exibe os resultados
        Console.WriteLine("\nOs números inseridos são:");
        Console.WriteLine($"W = {numeros.W}");
        Console.WriteLine($"Waprox = {numeros.Waprox}");
        Console.WriteLine($"Z = {numeros.Z}");
        Console.WriteLine($"Zaprox = {numeros.Zaprox}");

        Console.WriteLine();
        Console.WriteLine($"Erro absoluto (EabsW) = {eabsW}");
        Console.WriteLine($"EroLW = {erolW}");
        
        Console.WriteLine();

        Console.WriteLine($"Erro absoluto (EabsZ) = {eabsZ}");
        Console.WriteLine($"EroLZ = {erolZ}");
        Console.WriteLine();

        Console.WriteLine($"Soma dos Erros Relativos = {somaErros}");
    }
}

using System;

namespace ExemploNumeros
{
    // Definição da classe Numeros
    public class Numeros
    {
        public float W { get; set; }
        public float Waprox { get; set; }
        public float Z { get; set; }
        public float Zaprox { get; set; }

        // Método para calcular o erro absoluto
        public float CalcularEabsW()
        {
            return Math.Abs(W - Waprox);
        }

        // Método para calcular EroL
        public float CalcularEroLW()
        {
            float EabsW = CalcularEabsW();
            return EabsW / Waprox;
        }

        // Método para calcular o erro absoluto
        public float CalcularEabsZ()
        {
            return Math.Abs(Z - Zaprox);
        }

        // Método para calcular EroL
        public float CalcularEroLZ()
        {
            float EabsZ = CalcularEabsZ();
            return EabsZ / Zaprox;
        }

        // Método para calcular a soma dos erros relativos
        public float SomaDosErrosRelativos()
        {
            float erolW = CalcularEroLW();
            float erolZ = CalcularEroLZ();

            // Verifica se a soma dos denominadores é zero
            if ((Waprox + Zaprox) == 0) throw new DivideByZeroException("A soma de Waprox e Zaprox não pode ser zero.");

            // Calcula a soma dos erros relativos conforme especificado
            return (Waprox / (Waprox + Zaprox) * erolW) + (Zaprox / (Zaprox + Waprox) * erolZ);
        }
    }
}
