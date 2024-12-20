using System;

namespace CarSimulation
{
    //Ata Güler 225040071
    //Yakıt Türü
    public enum FuelType
    {
        Gasoline,
        Diesel,
        Electric,
        Hybrid
    }

    // Aktarma Organları
    public enum Drivetrain
    {
        FrontWheelDrive,
        RearWheelDrive,
        AllWheelDrive
    }

    // Motorlar
    public class Engine
    {
        public int Horsepower { get; private set; }
        public double Displacement { get; private set; } // Liters

        public Engine(int horsepower, double displacement)
        {
            Horsepower = horsepower;
            Displacement = displacement;
        }

        public void Start()
        {
            Console.WriteLine("Engine is starting...");
        }

        public void Stop()
        {
            Console.WriteLine("Engine is stopping...");
        }
    }

    // Depolar
    public class FuelTank
    {
        public FuelType Fuel { get; private set; }
        public double Capacity { get; private set; } // Liters
        public double CurrentLevel { get; private set; }

        public FuelTank(FuelType fuel, double capacity)
        {
            Fuel = fuel;
            Capacity = capacity;
            CurrentLevel = capacity; // Assume tank is full at initialization
        }

        public void Consume(double amount)
        {
            if (CurrentLevel - amount >= 0)
            {
                CurrentLevel -= amount;
                Console.WriteLine($"Consumed {amount}L of fuel. Remaining: {CurrentLevel}L.");
            }
            else
            {
                Console.WriteLine("Not enough fuel!");
            }
        }
    }

    // Vites
    public class Transmission
    {
        public string Type { get; private set; } // e.g., Automatic or Manual
        public int Gears { get; private set; }

        public Transmission(string type, int gears)
        {
            Type = type;
            Gears = gears;
        }

        public void ShiftGear(int gear)
        {
            if (gear > 0 && gear <= Gears)
            {
                Console.WriteLine($"Shifted to gear {gear}.");
            }
            else
            {
                Console.WriteLine("Invalid gear!");
            }
        }
    }

    // Şasiler
    public class Chassis
    {
        public string BodyType { get; private set; } // e.g., Sedan, SUV, Hatchback
        public string Color { get; private set; }

        public Chassis(string bodyType, string color)
        {
            BodyType = bodyType;
            Color = color;
        }

        public void Paint(string newColor)
        {
            Color = newColor;
            Console.WriteLine($"The car has been repainted to {Color}.");
        }
    }

    // Araçkar
    public class Car
    {
        public string Model { get; private set; }
        public Engine Engine { get; private set; }
        public FuelTank FuelTank { get; private set; }
        public Transmission Transmission { get; private set; }
        public Chassis Chassis { get; private set; }
        public Drivetrain Drivetrain { get; private set; }

        public Car(string model, Engine engine, FuelTank fuelTank, Transmission transmission, Chassis chassis, Drivetrain drivetrain)
        {
            Model = model;
            Engine = engine;
            FuelTank = fuelTank;
            Transmission = transmission;
            Chassis = chassis;
            Drivetrain = drivetrain;
        }

        public void Drive()
        {
            Console.WriteLine($"Driving the {Model}...");
            Engine.Start();
            FuelTank.Consume(5); // Örnek Yakıt Tüketimleri
        }

        public void Park()
        {
            Console.WriteLine($"Parking the {Model}...");
            Engine.Stop();
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            // Örnek Companentler
            var engine = new Engine(200, 2.0); 
            var fuelTank = new FuelTank(FuelType.Gasoline, 50); 
            var transmission = new Transmission("Automatic", 6); 
            var chassis = new Chassis("Sedan", "Red"); 

            // Araba oluşturma kısmı
            var car = new Car("Toyota Camry", engine, fuelTank, transmission, chassis, Drivetrain.FrontWheelDrive);

            // Oyunun Simülasyonu
            car.Drive();
            car.Transmission.ShiftGear(3);
            car.Park();
        }
    }
}
