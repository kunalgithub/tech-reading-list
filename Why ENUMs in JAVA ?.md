Why Enum Exists? 

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
         .filter( account -> account.getType().equalsIgnoreCase(ACCOUNTS.SAVINGS)) //Psst
         .forEach(accont->System.out.println(Constants.ACCOUNTS.SAVINGS+"=>"+account))
```

Conclusion #1: Nothing here much. 

What if I want to know all the Account Types in my Project, So list all constants 

   ```
     String[] ACCOUNT_TYPES = {ACCOUNTS.SAVINGS, ACCOUNTS.CURRENT, ACCOUNTS.FIXED_DEPOSIT};
   ```
Observation: Now the hard coding shows
Conclusion #2: Something Odd? 
