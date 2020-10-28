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

#### Other alternative appraches:

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
