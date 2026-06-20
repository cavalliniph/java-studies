# Solução com interfaces

Criar um contrato (interface) `TaxService` permite redistribuir responsabilidades entre os serviços `RentalService` e `BrazilTaxService`:

```java
// model.services.BrazilTaxService

public class BrazilTaxService implements TaxService {
    public double tax(double amount) {
        if (amount <= 100.0) {
            return amount * 0.2;
        }
        return amount * 0.15;
    }
}
```

```java
// model.services.TaxService

public interface TaxService {

    double tax(double amount);
    
}
```

```java
//model.services.RentalService

public class RentalService {
    private Double pricePerHour;
    private Double pricePerDay;

    private TaxService taxService;

    public RentalService(
            Double pricePerHour,
            Double pricePerDay,
            TaxService taxService
    ) {
        this.pricePerHour = pricePerHour;
        this.pricePerDay = pricePerDay;
        this.taxService = taxService;
    }

    //...
}
```
