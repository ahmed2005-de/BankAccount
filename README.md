# BankAccount
using BankApp.Classes;



try
{
    var b = new BankAccount("Savings", 300);
    b.Deposit(200);
    b.Withdraw(100);
    Console.WriteLine(b.Name);
    Console.WriteLine(b.Balance);
    Console.WriteLine(b.HasPositiveBalance);
}
catch(ArgumentException a)
{
    Console.WriteLine($"error: {a.Message}");
}

namespace BankApp.Classes;

public class BankAccount
{
    private string name;
    public string Name
    {
        get { return name; }

        set
        {
            if (!string.IsNullOrWhiteSpace(value))
            name = value;
            else 
                throw new ArgumentException(nameof(value) , "Name cannot be empty" ); 
        }
    }

    private decimal balance;

    public decimal Balance
    {
        get => balance;

        set
        {
            if (value >= 0)
                balance = value;
            else 
            throw new ArgumentOutOfRangeException(nameof(value) , "Balance Cannot Be Negative");
        }
    }

    public bool HasPositiveBalance => (balance > 0);

    public string Number { get; set; }

    public BankAccount(string name, decimal balance)
    {
        Name = name;
        balance = balance;
    }

    public BankAccount() : this("personal",100)
    {}

    public void Deposit(decimal amount)
    {
        if (amount > 0)
            balance += amount;
    }

    public void Withdraw(decimal amount)
    {
        if (amount > 0)
            if (amount <= balance)
                balance -= amount;
    }
}

<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net10.0</TargetFramework>
    <ImplicitUsings>enable</ImplicitUsings>
    <Nullable>enable</Nullable>
  </PropertyGroup>

</Project>
