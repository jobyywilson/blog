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
