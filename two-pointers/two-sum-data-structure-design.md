# 607. Two Sum - Data structure design

> Design and implement a TwoSum class. It should support the following operations:`add`and`find`.
>
> `add`- Add the number to an internal data structure.  
> `find`- Find if there exists any pair of numbers which sum is equal to the value.
>
> **Example**
>
> ```
> add(1); add(3); add(5);
> find(4) // return true
> find(7) // return false
> ```



```java
public class TwoSum {
    private List<Integer> numbers;
    
    public TwoSum() {
        numbers = new ArrayList<Integer>();
    }
    
    // Add the number to an internal data structure.
    public void add(int number) {
        // Write your code here
        this.numbers.add(number);
    }

    // Find if there exists any pair of numbers which sum is equal to the value.
    public boolean find(int value) {
        // Write your code here
        Set<Integer>  set = new HashSet<Integer>();
        for (int i = 0; i < numbers.size(); i++) {
            int required = value - numbers.get(i);
            if (set.contains(required)) {
                return true;
            }
            set.add(numbers.get(i));
        }
        return false;
    }
}


// Your TwoSum object will be instantiated and called as such:
// TwoSum twoSum = new TwoSum();
// twoSum.add(number);
// twoSum.find(value);
```



