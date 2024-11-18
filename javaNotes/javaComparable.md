java, comparable

# `Comparable Interface`

- built in `funtional interface`
- has only 1 method: `compareTo(Object)`
- part of the `java.lang` package


## `compareTo()` method
- helps ordering objects of a class that implements it
- is used to compare the current object to the one passed to it
- returns 0 if object are the same
- positive integer if the current object is greater
- negative integer if the current object is lesser

```java
class Employee implements Comparable {

    @Override
    public int compareTo(Employee employee) {
        if(employeeId = employee.employeeId)
            return 0;
        else if(employeeId > employee.employeeId)
            return 1;
        else
            return 1;
    }
}

```

## Example
```java
import java.util.Arrays;
import java.util.Comparator;
import java.util.List;

// Implementation class for the Comparator interface
class SortImplementationOne implements Comparator<String> {

	//compare method overridden 
	@Override
	public int compare(String o1, String o2) {
        // uses natural ordering
		return o1.compareTo(o2);
	}
}

// Another implementation class for the Comparator interface
class SortImplementationTwo implements Comparator<String> {

	//compare method overridden
	@Override
	public int compare(String o1, String o2) {
		return o1.length()-o2.length();
	}
}

class DemoSort {

	public static void main(String[] args) {
		List<String> employeeNames = Arrays.asList("Rachael","Ross","Monica",
                "Chandler","Joey","Phoebe");
		
		//Displaying employeeNames before sorting
		System.out.println(employeeNames);
		
		// list.sort() takes the implementation of Comparator interface for inducing the ordering
		Comparator<String> compare1 = new SortImplementationOne();
		employeeNames.sort(compare1);
		
		//Displaying employeeNames after sorting based on natural ordering
		System.out.println(employeeNames);
		
		// list.sort() takes another implementation of Comparator interface for inducing the ordering
		Comparator<String> compare2 = new SortImplementationTwo();
		employeeNames.sort(compare2);
		
		//Displaying employeeNames after sorting based on length of each element
		System.out.println(employeeNames);
	}
}
```

## Example

```java

Class Product implements Comparable<Product> {
    String productId;
    double price;
    
    Product() {}
    Product(String n, double a) {
        productId = n;
        price = a;
    }
    
    public int compareTo(Product product) {
        if(this.price == product.price) return 0;
        else if(this.price > product.price) return 1;
        else return -1;
    }k
}
```

