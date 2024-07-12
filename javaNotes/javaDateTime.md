java, date, time

# Date Time API
- `java.time` package


## LocalDate
- immutable class
- represents dates with default format `yyyy-MM-dd`
- does NOT store time or time-zone


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

