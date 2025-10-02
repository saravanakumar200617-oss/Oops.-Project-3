import java.util.*;

class NumberBox<T extends Number> {
    private T value;

    public NumberBox(T value) {
        this.value = value;
    }

    public T get() {
        return value;
    }

    public double doubleValue() {
        return value.doubleValue();
    }
}

public class BoundedTypesDemo {
    
    // Upper bounded wildcard → only read
    public static double sumList(List<? extends Number> list) {
        double sum = 0.0;
        for (Number n : list) {
            sum += n.doubleValue();
        }
        return sum;
    }

    // Lower bounded wildcard → only add
    public static void fillWithIntegers(List<? super Integer> list) {
        list.add(10);
        list.add(20);
        list.add(30);
    }

    public static void main(String[] args) {
        // Using bounded generic class
        NumberBox<Integer> ibox = new NumberBox<>(100);
        NumberBox<Double> dbox = new NumberBox<>(25.75);

        System.out.println("Integer Box double value = " + ibox.doubleValue());
        System.out.println("Double Box double value = " + dbox.doubleValue());

        // Using bounded methods
        List<Integer> intList = Arrays.asList(1, 2, 3, 4);
        List<Double> doubleList = Arrays.asList(2.5, 3.5, 4.0);

        System.out.println("Sum of Integer List = " + sumList(intList));
        System.out.println("Sum of Double List = " + sumList(doubleList));

        List<Number> numbers = new ArrayList<>();
        fillWithIntegers(numbers);
        System.out.println("Numbers after filling = " + numbers);
    }
}
