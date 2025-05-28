# Currency Exchange Rate Converter

## Project Overview

This project is a **Currency Exchange Rate Converter** built using **C#**, designed to convert an amount from one currency to another. It supports multiple currencies and optionally connects to live exchange rate APIs or uses fixed/local data for conversions.

---

## Features

- Convert between multiple world currencies
- Support for both current and historical exchange rates
- Console or Windows-based UI options (WinForms/WPF)
- Modular design using interfaces for extensibility
- Optional API integration for real-time exchange rates
- Input validation and user-friendly feedback

---

## Objectives

- Develop a reliable and functional currency converter
- Implement accurate currency conversion logic
- Ensure a clean and user-friendly interface
- Validate inputs and manage errors gracefully
- Support future enhancements like charts, alerts, and history

---

## Technologies Used

- **Language**: C#
- **UI Options**: Console App / WinForms / WPF
- **Data Source**: Fixed rates, local files (JSON/XML), or online APIs (e.g., Fixer.io, ECB)

---

## Project Structure

### Classes

#### `CurrencyConverter`

Handles the core logic for converting currency using a provided exchange rate source.

```csharp
public class CurrencyConverter
{
    public decimal Amount { get; set; }
    public string SourceCurrency { get; set; }
    public string TargetCurrency { get; set; }
    public DateTime? RateDate { get; set; }

    private IExchangeRateProvider _rateProvider;

    public CurrencyConverter(IExchangeRateProvider rateProvider)
    {
        _rateProvider = rateProvider;
    }

    public decimal Convert()
    {
        decimal rate = _rateProvider.GetExchangeRate(SourceCurrency, TargetCurrency, RateDate);
        return Amount * rate;
    }

    public static Dictionary<string, string> GetAvailableCurrencies()
    {
        return new Dictionary<string, string>
        {
            {"USD", "US Dollar"},
            {"EUR", "Euro"},
            {"GBP", "British Pound"},
            {"JPY", "Japanese Yen"}
        };
    }
}
