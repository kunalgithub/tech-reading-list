## Why Enum Exists? 

Thought Experiment:  ENUM does not exist. So, could you write Java Code and know the implications? 

Functional Case: When fetching account data from a Bank's API, Filter Only Certain Types of Account Type 

What are account types in Banking? Typical Example ( lower case or all upper case ) 

  - SAVINGS
  - CHECKINGS 
  - OVERDRAFT

The bank's API Response can typically identify the type of Accounts by using the String above or by number. 

- SAVINGS - 01
- CHECKINGS - 02
- OVERDRAFT - 03

Define Constants

```
public class Constants {
  public static final String SAVINGS = "SAVINGS";
  public static final String CHECKINGS = "CHECKINGS";
  public static final String OVERFRAFT = "OVERFRAFT";
}
```
The constants can be tied more closely to the definition of our Domain, so 

```
public class ACCOUNTS {
  public static final String SAVINGS = "SAVINGS";
  public static final String CHECKINGS = "CHECKINGS";
  public static final String OVERDRAFT = "OVERDRAFT";
}
```


So effectively, when a response comes from the bank's API, I can filter using it. 

```
response.getAccounts()
         .steam()
         .filter( account -> account.getType().equalsIgnoreCase(Constants.SAVINGS))
         .forEach(accont->System.out.println(Constants.SAVINGS+"=>"+account))
```
Modifying it to mimic Domain closely, I can re-write 

```
response.getAccounts()
         .steam()
         .filter( account -> account.getType().equalsIgnoreCase(ACCOUNTS.SAVINGS)) //Psst!
         .forEach(accont->System.out.println(Constants.ACCOUNTS.SAVINGS+"=>"+account))
```

**Conclusion #1** : Nothing here much. 


`Business Scenario`: What if I want to know all the Account Types in my Project, So list all constants.
 Print all the account types using the SAVINGS, CURRENT, and OVERDRAFT types.
   
   ```
      String[] ACCOUNT_TYPES = {ACCOUNTS.SAVINGS, ACCOUNTS.CURRENT, ACCOUNTS.OVERDRAFT};
     .steam()filter( account -> Arrays.asList(ACCOUNT_TYPES).contains(account.getType())) //Psst!
     .forEach(accont->System.out.println(Constants.ACCOUNTS.SAVINGS+"=>"+account))
   ```
**Observation**: Now, all the places where such business requirements must be fulfilled have hard coding involved. 
Bring down the `Code Maintenancblity index`. [I do not know whether such an index is present ;) ] 

**Conclusion #2**: Code Pattern brought about by such Language Specification makes Maintainence hard. 

`Business Scenario`: Aggregate all the savings accounts from all the Verticals of the Business ( Line of Business ) 

 Here is the flag that recognises the per LOB. 
   - LOB_ALPHA - Have a flag for SAVINGS as "SAVINGS"
   - LOB_BETA - Have a flag for SAVINGS as "015"

I was hoping you wouldn't ask me why because different systems use different technologies for Storage. 

I can write the code as 
```
 public class ACCOUNTS {
     public static final Map<String,String> LOB_MAPPING = Map.of(LOB_ALPHA,ACCOUNT_TYPES,LOB_BETA,ACCOUNT_TYPES_BETA)
  } 
```
You can debate the way code can be written in other forms. 

**Conclusion #3**: We see that within the language construct, representing 
- Representing Business Information becomes a hack. 
- and Maintainability is time-consuming.  

**Conclusion #4**: Languages Built for Enterprise should introduce a language construct to simplify the Business Information. 

**Thought Experiment is over**

----
Let's look at the enum specification and check if we can find some mail archives on the Internet. 
I will utilise **Grok3 Beta 22-March-2025** to find information faster with the Advent of GenAI. 

**The below information is where information is sought through GenAI only**

- ENUM was introduced in Java 5.0
- Origins of the Enum Concept: The idea of enumerated types predates Java, with roots in languages like Pascal, which introduced them in the late 1960s and early 1970s to define named constants, though without the "enum" keyword. C later popularized the concept with the "enum" keyword for named integer constants. Java enhanced this idea in 2004, making enums full-fledged classes with additional features like methods and constructors.

>> Type safety was a vital aspect I missed in my `Thought Experiment`.
>> This means I looked at the code smells the Application Produces without Enum

**Conclusion from Grok**

``` Java's ENUM is considered type-safe because it ensures that a variable can only hold one of the predefined constants declared within the enum```

Additional Points from my side 

  - Enterprise Software Life can be multi-year
  - Software is maintained by people who move around
  - Large code bases are maintenance-heavy and are suspectable to big bugs with small lines of change
  - Code Review of such can become Error Prone.

Grok suggested that the concept of enum was first introduced in PASCAL, and Grok concludes that 
```
In summary, Pascal introduced enumerated types to improve code readability, maintainability, and type safety.

```
**ENDING NOTE** 
- While I was Right on some aspects, type safety was missed
- It might have been missed as the bias would have come from the fact that the code would be reviewed at merge time.
- If your day-to-day activity is coding, do you need a time when you can see things from a bird's eye view? 


*** END OF STORY ** 

