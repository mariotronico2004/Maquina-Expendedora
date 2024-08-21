# Maquina-Expendedora
Maquina expendedora con respecto a la materia de "Técnicas de Programacion", aqui el codigo: 

using System;
using System.Collections.Generic;

class VendingMachine
{
    private Dictionary<string, (double price, int quantity)> products;

    public VendingMachine()
    {
        products = new Dictionary<string, (double price, int quantity)>
        {
            {"Chips", (1.50, 10)},
            {"Soda", (1.00, 5)},
            {"Candy", (0.75, 20)}
        };
    }

    public void DisplayProducts()
    {
        Console.WriteLine("Productos disponibles:");
        foreach (var item in products)
        {
            Console.WriteLine($"{item.Key} - ${item.Value.price} (Cantidad: {item.Value.quantity})");
        }
    }

    public void BuyProduct(string productName, double amountInserted)
    {
        if (products.ContainsKey(productName))
        {
            var (price, quantity) = products[productName];

            if (quantity == 0)
            {
                Console.WriteLine("Lo siento, el producto está agotado.");
                return;
            }

            if (amountInserted < price)
            {
                Console.WriteLine("No hay suficiente dinero. Se requiere ${0}.", price);
                return;
            }

            // Si llega aquí, el producto se puede dispensar
            products[productName] = (price, quantity - 1);
            double change = amountInserted - price;
            Console.WriteLine($"Has comprado {productName}. Cambio: ${change:F2}");
        }
        else
        {
            Console.WriteLine("Producto no encontrado.");
        }
    }
}

class Program
{
    static void Main()
    {
        VendingMachine vendingMachine = new VendingMachine();
        
        while (true)
        {
            vendingMachine.DisplayProducts();

            Console.Write("Ingresa el nombre del producto que deseas comprar (o 'salir' para terminar): ");
            string productName = Console.ReadLine();
            if (productName.ToLower() == "salir")
                break;

            Console.Write("Ingresa el monto de dinero insertado: ");
            if (double.TryParse(Console.ReadLine(), out double amountInserted))
            {
                vendingMachine.BuyProduct(productName, amountInserted);
            }
            else
            {
                Console.WriteLine("Monto inválido. Inténtalo de nuevo.");
            }

            Console.WriteLine();
        }
    }
}



![image](https://github.com/user-attachments/assets/819037a3-8a58-4ab7-bd08-3565254d9871)

