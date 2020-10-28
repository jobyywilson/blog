---
layout: post
title: Java 9 - Factory methods for Collections
---

Java 9 Collection library introduced static factory methods for List, Set and Map interface.

### Before Java 9

If you want to create a small, unmodifiable collection(say, a set) involves constructing it, storing it in a local variable, and invoking add() on it several times, and then wrapping it. For example,

    Set<String> set = new HashSet<>();
    set.add("a");
    set.add("b");
    set.add("c");
    set = Collections.unmodifiableSet(set);

#### Other alternative approaches:

Using copy constructor from another collection:

    Set<String> set = Collections.unmodifiableSet(new HashSet<>(Arrays.asList("a", "b", "c")));
    
Using the so-called "double brace" technique:

    Set<String> set = Collections.unmodifiableSet(new HashSet<String>() {{
        add("a"); add("b"); add("c");
    }});

Using Java 8 API streams:

    Set<String> set = Collections.unmodifiableSet(Stream.of("a", "b", "c").collect(toSet()));
    
### After Java 9

    Set<String> set = Set.of("a", "b", "c");
    
This same feature is also there for List and Map.

List example:

    List<String> stringList = List.of("a","b","c");
    
Map example:

    Map<String,Integer> stringMap = Map.of("a",1,"b",2,"c",3);

where (a,1),(b,2),(c,3) are the key value pairs
    

### API Overview

For List :

| Various `of` methods              | Description                                         |
|----------------------|-----------------------------------------------------|
| List.of()            | Creates an empty list                               |
| List.of(e1)          | Creates a list with one elements                     |
| List.of(e1,e2)       | Creates a list with two elements                     |
| ......               | Separate methods for creating list from 3 to 10 elements |
| List.of(e1,e2,..e10) | Creates a list with 10 elements                      |
| List.of(elements ..) | Creates a list with arbitrary number of elements    |

For Set :

| Various `of` methods               | Description                                         |
|----------------------|-----------------------------------------------------|
| Set.of()            | Creates an empty set                               |
| Set.of(e1)          | Creates a set with one element                     |
| Set.of(e1,e2)       | Creates a set with two elements                     |
| ......               | Separate methods for creating set from 3 to 10 elements |
| Set.of(e1,e2,..e10) | Creates a set with 10 elements                      |
| Set.of(elements ..) | Creates a set with arbitrary number of elements    |

For Map:

| Various `of` methods               | Description                                         |
|----------------------|-----------------------------------------------------|
| Map.of()            | Creates an empty map                               |
| Map.of(k1,v1)          | Creates a map with one pair                     |
| Map.of(k1,v1,k2,v2)       | Creates a map with two pairs                     |
| ......               | Separate methods for creating map from 3 to 10 pairs |
| Map.of(k1,v1,,..k10,v10) | Creates a map with 10 pairs                      |

`Map.of` method does not support arbitrary number of elements. So if you want to create a map with more than 10 pairs then we have do something else.

That is by creating a Map.entry instance.
    import static java.util.Map.entry;
    Map.entry(k,v)

To create a Map with an arbitrary number of mappings,

Map.ofEntries(entry(k1,v1), entry(k2,v2), ...)
