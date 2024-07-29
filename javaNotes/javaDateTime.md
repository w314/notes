java, date, time

# Date Time API
- `java.time` package


## LocalDate
- `immutable` class
- represents dates with default format `yyyy-MM-dd`
- does **NOT** store time or time-zone


```java
// now() - returns current date
LocalDate today = LocalDate.now(); /
System.out.println(today); 
		
// of() return LocalDate object         
LocalDate dateObj = LocalDate.of(1997, 8, 29);  
```

To format the date use `DateTimeFormatter`
```java
LocalDate dateObj = LocalDate.of(1997, 8, 29);
				
DateTimeFormatter df = DateTimeFormatter.ofPattern("dd/MM/yy"); 
		
System.out.println(df.format(dateObj)); //output 29/08/97
```

### `LocalDate` Methods
- `LocalDate LocalDate.now()`

Add / deduct days/months/years
- `plusDays` / `minusDays()`
- `plusMonths` / `minusMonths()`
- `plusYears()` / `minusYears()`
- all take Long parameters
- all return `LocalDate` 

```java

//Invoking the static now() will return the current date from the system clock
//LocalDate provides the output in the form of YYYY-MM-DD
LocalDate today = LocalDate.now();
System.out.println(today);

/*
		 * To display any date in default format we use of() method.
		 * of() takes parameters as public static LocalDate of(int year,Month month,int dayOfMonth)(where Month is enum )
		 * Or public static LocalDate of(int year,int month,int dayOfMonth)
		 * This returns a LocalDate with the specified year, month and day-of-month
		*/
		System.out.println();
		System.out.println("************"+"of()"+"************");
		System.out.println("LocalDate.of(2018, 8, 29) :- "+LocalDate.of(2018, 8, 29));
		System.out.println("LocalDate.of(2017,Month.APRIL, 29) :- "+LocalDate.of(2017,Month.APRIL, 29));
		
		/*
			To access the date information we have certain methods like getYear(),getMonth(),getDayOfMonth() etc.
		
		*/
		System.out.println();
		System.out.println("***********DateTimeFormater***********");
		LocalDate date = LocalDate.parse("13 Feb, 2020", DateTimeFormatter.ofPattern("dd MMM, yyyy"));
		System.out.println(date.format(DateTimeFormatter.ofPattern("dd-MMM-yyyy")));
		System.out.println("Input Format is 13 Feb, 2020 \nOutput Format :-  "+date);
		
		/*
			.format() method formats the date according to user defined pattern.
		
		*/
		String dateString = date.format(DateTimeFormatter.ofPattern("dd/MMM/uuuu"));
		System.out.println(dateString);
		
		/*
			The DateTimeFormatter class in Java is used for parsing dates in different formats.
			ofPattern method will create a formatter based on the pattern given by the programmer. 
			For example, d MMM yyyy will format 2011-12-03 as '3 Dec 2011'. 
		*/
		
		
		System.out.println();
		System.out.println("************"+"Functions to access date information"+"************");
		System.out.println("Today's Date :- "+LocalDate.now());
		System.out.println("Month in Today's Date :- "+LocalDate.now().getMonth());
		System.out.println("What is the current year going on .... ? :- "+LocalDate.now().getYear());
		System.out.println("Which day is today ? :- "+LocalDate.now().getDayOfWeek());
		
		/*
			getDayOfWeek() & getMonth() :- returns an enum instead of int value.
			To get int value, we can use getValue() methods
			
			Try :- System.out.println("Month in Today's Date :- "+LocalDate.now().getMonth().getValue());
				   System.out.println("Which day is today ? :- "+LocalDate.now().getDayOfWeek().getValue());

		*/
		
		
		/*
			Following are methods for localdate calculations 
			plusDays(),plusWeeks(),plusMonths(),plusYears(),minusDays(),minusWeeks(),minusMonths,()minusYears()
			All of these methods take parameters having Long datatype
		*/
		System.out.println();
		System.out.println("************"+"LocalDate Calculations"+"************");
		System.out.println("Today's Date :- "+LocalDate.now());
		System.out.println("Date after 7 days ?	 => "+LocalDate.now().plusDays(7));
		System.out.println("Date after 7 months ?	 => "+LocalDate.now().plusMonths(7));
		System.out.println("Date after 7 Years ?	 => "+LocalDate.now().plusYears(7));
		System.out.println("Date after 7 weeks ?	 => "+LocalDate.now().plusWeeks(7));
		
		System.out.println();
		/*
			Try :- 
					Find the date 20 days ago and 4 months ago and 40 years ago
		*/	
		
		System.out.println();
		System.out.println("************"+"Difference using ChronoUnit"+"************");
		LocalDate dateObj = LocalDate.of(1997, Month.FEBRUARY, 15);
		System.out.println("Difference Between dateObj and today's date in number of Years");
		System.out.println(ChronoUnit.YEARS.between(dateObj, LocalDate.now()));
		// Calculate the number of days between dateObj and today's date
		
		/*
			We can also modify the date using ChronoUnit
		
		*/
		System.out.println();
		System.out.println("Modification of date using ChronoUnit :- ");
		System.out.println("Today's date :- "+LocalDate.now());
		System.out.println("Date After 5 days :- "+LocalDate.now().plus(5,ChronoUnit.DAYS));
		//Try adding months and years in the current date. 
		
		System.out.println();
		System.out.println("until() with ChronoUnit");
		LocalDate todayObj = LocalDate.now();
		LocalDate date1 = LocalDate.of(2014,5,25);
		System.out.println("Difference between todayObj and date1(in terms of Number of Days) :- "+date1.until(todayObj,ChronoUnit.DAYS));
		//calulcate the difference in terms of months and years
		
		/*
			To Compare two dates we also have compareTo() method 
			Method Signature of compareTo() :- int compareTo(chronoLocalDate date)
			
			It returns the value 0 if the argument Date is equal to this Date.
			It returns a value less than 0 if this Date is before the Date argument.
			It returns a value greater than 0 if this Date is after the Date argument.
			
			Try Comparing today's date with date1 using compareTo()
		*/
		System.out.println();
		System.out.println("************"+"isAfter() and isBefore()"+"************");
		LocalDate dateFirst = LocalDate.of(2018, 2,21);
		LocalDate dateSecond = LocalDate.of(2018, 2,20);
		
		System.out.println("dateFirst.isBefore(dateSecond) :- "+dateFirst.isBefore(dateSecond));
		System.out.println("dateFirst.isAfter(dateSecond) :- "+dateFirst.isAfter(dateSecond));
		
	}

}


```


Calculate difference between dates
```java
LocalDate today = LocalDate.now();
LocalDate newDateObj = today.minusWeeks(39);
System.out.println(ChronoUnit.DAYS.between(newDateObj,today));  //273
//between() calculates the amount of time between specified date objects
System.out.println(ChronoUnit.MONTHS.between(newDateObj,today)); //8
//compareTo() compares this date with specified date
System.out.println(newDateObj.compareTo(today)); //-1 
```
`ChronoUnit`
- enum
- provides unit based access to manipulate date, time or date-time


Get details of a date
```java
// get day



```

Compare dates:
- `int compareTo()

## Examples

what is the output?
```java
LocalDate date = LocalDate.of(2018,4,18);
date = date.minusDays(18);
date.minusMonths(1);
System.out.println(date);
```
2018-03-31
- `LocalDate` is an immutable class
- with `date = date.minusMonths(1);` it would output 2018-02-28
