 ### Assignemnt - 1
Typical product database consists of two types of product components — product categories and product items. 
A product category is generally  contain product items and also other product categories as its subcategories. Example Product Categories: 

- Computers
- Desktops
- Laptops
- Peripherals 
- Printers
- Cables 

The Computers product category contains both the Desktops and the Laptops product categories as its subcategories. The Desktop category can contain a product item such as Compaq Presario 5050. Product items are usually individual, in the sense that they do not contain any product component within. 
Design and implement an PricingCalculator  to list the dollar value of a product component or Product Category.

![Assignment1](https://github.com/shkalaria/philips-july-dp-2022/blob/main/Assignments/Assignment_1.PNG)

### Assignment - 2
```
public class OnlineCart
{
    public void CheckOut(PaymentType paymentType)
    {
        switch(paymentType)
        {
            case PaymentType.CreditCard:
                    ProcessCreditCardPayment();
                    break;
            case PaymentType.Paypal:
                    ProcessPaypalPayment();
                    break;
            case PaymentType.GoogleCheckout:
                    ProcessGooglePayment();break;
            case PaymentType.AmazonPayments:P
                    ProcessAmazonPayment();
                    break;
        }
    }
    private void ProcessCreditCardPayment()
    {
        Print("Credit card payment chosen");
    }
    private void ProcessPaypalPayment(){
        Print("Paypal payment chosen");
    }
    private void ProcessGooglePayment()
    {
        Print("Google payment chosen");
    }
    private void ProcessAmazonPayment()
    {
        Print("Amazon payment chosen");
    }
}
```

![Assignment2](https://github.com/shkalaria/philips-july-dp-2022/blob/main/Assignments/Assignment_2.PNG)

### Assignment - 3
#### CNC Monitoring and Alerting

We need a solution to interpret data coming out of a _CNC-machine monitor_.
Our purpose is to alert when something needs attention.
The alert needs to include information on the area that needs attention -
the machine or the environment.
The personnel that need to be alerted are different in each case.

A basic idea of CNC machines can be seen [here](https://en.wikipedia.org/wiki/Numerical_control).
Keeping these machines safe and reliable is vital in any manufacturing unit.

#### Monitored data

The _CNC-machine monitor_ gives the following data:

- Operating temperature: Temperature around the CNC machine in Celsius.
Reported every half-hour. Need to alert if it goes beyond 35 degrees.

- Part-dimension variation: In mm. A variation of more than 0.05 mm needs attention
(example: a drill-bit in the machine may need replacement)

- Duration of continuous operation: Reported in minutes.
Updated once every 15 minutes.
More than 6 hours of continuous operation requires attention.

- Self-test status-code, reported at startup

| Code | Meaning |
|---:|---|
|0xFF|All ok|
|0x00|No data (examples: no power, no connection to the data-collector)|
|0x01|Controller board in the machine is not ok|
|0x02|Configuration data in the machine is corrupted|

Assume that the above data is monitored and passed-on to your program.
You can choose to take the inputs as function calls to your program, or as events.

#### Expected outputs

The program needs to indicate if there is a need for attention.

When there is a need to attend,
it needs to offer an initial diagnosis,
to help in alerting the appropriate personnel:
It needs to convey whether the machine needs attention,
or if its environment needs attention.

#### Design-it

![Assignment3](https://github.com/shkalaria/philips-july-dp-2022/blob/main/Assignments/Assignment_3.PNG)

#### Assignment -4 
---
https://github.com/venu-shastri/design-patterns-summary/blob/main/DEBT_CODE.docx

DEBT_CODE

<li> Violation of SRP
<li> Inheritance can be used
<br></br>

``` C++
class Icon
{
    float speed, glow, energy;
    int x, y;
    int subtype; // spinner, slider or hopper
 
    bool clockwise; // need for spinner
    bool expand; // need for spinner
    bool vertical; // need for slider
 
    int distance; // need for slider
    bool visible; // need for hopper
 
    int xcoord, ycoord; // need for hopper
 
    void spin() { }
 
    void slide() { }
 
    void hop() { }
    // constructor must set subtype: client must pass value
    public Icon(unsigned value)
    {
        subtype = value; // use enum for readability
        // and then use conditional to set associated fields
    }
    public void move()
    {
        if (subtype == 1) { spin(); }
        else if (subtype == 2)
        {
            slide();
        }
        else
        {
            hop();
        }
    }
}
```

#### Assignment 5
---
Let us build a sales reporting application for the management of a store with multiple departments. The features of the application include:

- Users should be able to select a specific department they are interested in.
- Upon selecting a department, two types of reports are to be displayed:
- Monthly report — A list of all transactions for the current month for the selected department.
- YTD sales chart — A chart showing the year-to-date sales for the selected department by month.
	
Whenever a different department is selected, both reports should be refreshed with the data for the currently selected department 

![Assignment5](https://github.com/shkalaria/philips-july-dp-2022/blob/main/Assignments/Assignment_5.PNG)

#### Assignemnt 6
---
Refactor Below Code and remove code pollution
``` C#
	public class ConcreteCalculator : ICalculator
{
    public int Add(int x, int y)
    {
        Print("Add(x={0}, y={1})", x, y);

        var addition = x + y;

        Print("result={0}", addition);

        return addition;
    }
}

```

Refactored Code :

``` C#
using System;

// decorator pattern or proxy pattern can be used

public interface ICalculator {
    int Add(int x, int y);
}

public class LogCalculatorDecorator: ICalculator {
    ICalculator _target;
    public LogCalculatorDecorator(ICalculator cal) {
        this._target = cal;
    }

    public int Add(int x, int y) {
        Console.WriteLine("Add(x={0},y={1})",x,y);
        int add = _target.Add(x,y);
        Console.WriteLine("result={0}", add);
        return add;
    }
}

public class ConcreteCalculator : ICalculator
{
    public int Add(int x, int y)
    {
        var addition = x + y;
        return addition;
    }
}

public class Program
{
    public static void Main() {
        ICalculator _cal = new ConcreteCalculator();
        _cal = new LogCalculatorDecorator(_cal);
        _cal.Add(10,20);
    }
}
```

#### Assignment - 7 
----
Let us consider an online job site that receives XML data files from different employers with current openings in their organizations. When the number of vacancies is small, employers can enter details online. When the number of vacancies is large, employers upload details in the form of an XML file. Once the XML file is received, it needs to be parsed and processed. Let us assume the XML file to have the following details: 
-  a.Job title
- b.Minimum qualifications
- c.Medical insurance 
- d.Dental insurance
- e.Vision care
- f.Minimum number of hours of work 
- g.Paid vacation 
- h.Employer name 
- i.Employer address In general

Details from (c) through (i) are all considered being the same for all jobs posted by a given employer. Apply the required pattern to design the process of parsing the input XML file and creating different JOB objects


**Flyweight pattern**

![Assignment7](https://github.com/shkalaria/philips-july-dp-2022/blob/main/Assignments/Assignment_7.PNG)
