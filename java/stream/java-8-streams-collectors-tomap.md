### In this quick tutorial we're going to cover [Collectors.toMap()](https://docs.oracle.com/javase/8/docs/api/index.html) method of Collectors class. This utility method of Collectors class used to collect Stream into a Map instance.

### Following are the overloaded method of toMap() present in Collectors class:-

````
public static <T,K,U> Collector<T,?,Map<K,U>> toMap(Function<? super T,? extends K> keyMapper,
                                                    Function<? super T,? extends U> valueMapper)
````

````
public static <T,K,U> Collector<T,?,Map<K,U>> toMap(Function<? super T,? extends K> keyMapper,
                                                    Function<? super T,? extends U> valueMapper,
                                                    BinaryOperator<U> mergeFunction)
````

````
public static <T,K,U,M extends Map<K,U>> Collector<T,?,M> toMap(Function<? super T,? extends K> keyMapper,
                                                                Function<? super T,? extends U> valueMapper,
                                                                BinaryOperator<U> mergeFunction,
                                                                Supplier<M> mapSupplier)
````

### Type Parameters:
**T** - the type of the input elements  
**K** - the output type of the key mapping function  
**U** - the output type of the value mapping function  
**M** - the type of the resulting Map  
 
### Parameters:
**keyMapper** - a mapping function to produce keys  
**valueMapper** - a mapping function to produce values  
**mergeFunction** - a merge function, used to resolve collisions between values associated with the same key, as supplied to Map.merge(Object, Object, BiFunction)  
**mapSupplier** - a function which returns a new, empty Map into which the results will be inserted

### Return
A Collector which collects elements into a Map whose keys are the result of applying a key mapping function to the input elements, and whose values are the result of applying a value mapping function to all input elements.

#### Notes:-
+ It is common for either the key or the value to be the input elements. In this case, the utility method *Function.identity()* may be helpful.
+ By default toMap() method return HashMap instance.

### Example:-

    class Person {
        private String firstName;
        private String lastName;
        private int age;
    
        ---getters and setters 
    }
    
### Create List of persons
    List<Person> persons = new ArrayList<>();
    persons.add(new Person("John", "Deo", 35);
    persons.add(new Person("Boos", "Deo", 40);
    persons.add(new Person("Ram", "D", 55);
    persons.add(new Person("Jan", "P", 60);
    
### Create person map firstName as key and age as value
    persons.stream().collect(Collectors.toMap(Person::getFirstName, Person::getAge));

### Create person map firstName as key and Person as value
    persons.stream().collect(Collectors.toMap(Person::getFirstName, Functions.identity()));
    
### Create person map Person as key and firstName as value
        persons.stream().collect(Collectors.toMap(Functions.identity(), Person::getFirstName));
    
### Create person map firstName as key and age as value. Use fullName if key having conflict
        persons.stream().collect(Collectors.toMap(Person::getFirstName, Person::getAge, (exiting, replacement) -> replacement.getFirstName() + " " + replacement.getlastName()));

### Create person map firstName as key and age as value. Use fullName if key having conflict and Store in Tree Map
        persons.stream().collect(Collectors.toMap(Person::getFirstName, Person::getAge, (exiting, replacement) -> replacement.getFirstName() + " " + replacement.getlastName(), TreeMap::new));


## If you want ConcurrentMap instance then either you can use supplier version of toMap() method by passing ConcurrentMap instance or use toConcurrentMap() version.

````
public static <T,K,U> Collector<T,?,Map<K,U>> toConcurrentMap(Function<? super T,? extends K> keyMapper,
                                                    Function<? super T,? extends U> valueMapper)
````

````
public static <T,K,U> Collector<T,?,Map<K,U>> toConcurrentMap(Function<? super T,? extends K> keyMapper,
                                                    Function<? super T,? extends U> valueMapper,
                                                    BinaryOperator<U> mergeFunction)
````

````
public static <T,K,U,M extends Map<K,U>> Collector<T,?,M> toConcurrentMap(Function<? super T,? extends K> keyMapper,
                                                                Function<? super T,? extends U> valueMapper,
                                                                BinaryOperator<U> mergeFunction,
                                                                Supplier<M> mapSupplier)
````
