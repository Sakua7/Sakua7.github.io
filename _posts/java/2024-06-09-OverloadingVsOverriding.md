---
title: Overloading vs Overriding
date: 2024-06-09 00:00:00 +0000
categories: [Java]
tags: [Java]
author: Sakua7
mermaid: true
---

## Overloading

- 같은 클래스 내부에서 같은 메서드 이름을 가지고 있지만 **매개변수의 타입 or 개수 or 순서가 다른 메서드**
<!-- A method within the same class that has the same method name but differs in parameter type, number, or order -->

- 어떤 메서드를 사용할지는 컴파일 단계에서 결정된다.
<!-- The determenation of which method to use is made at the compile time. -->

```java
// Overloading 예시
class MathOperations {
    // 정수 두 개의 합
    public int add(int a, int b) {
        return a + b;
    }

    // 실수 두 개의 합
    public double add(double a, double b) {
        return a + b;
    }

    // 정수 세 개의 합
    public int add(int a, int b, int c) {
        return a + b + c;
    }

    public static void main(String[] args) {
        MathOperations math = new MathOperations();
        System.out.println(math.add(5, 3));       // 정수 덧셈: 8
        System.out.println(math.add(5.0, 3.0));   // 실수 덧셈: 8.0
        System.out.println(math.add(1, 2, 3));    // 정수 세 개의 덧셈: 6
    }
}
```

## Overriding

- 상위 클래스에서 이미 정의된 메서드를 하위 클래스에서 **동일한 시그니처(메서드 이름, 매개변수 타입 및 변수)로** 다시 정의하는 것
<!-- It is the redefinition of a method in a subclass that was already defined in the superclass with the same signature(method name, parameter types, and order) -->

- @Overriding 어노테이션은 필수가 아니지만 컴파일 단계에서 실제 오버라이딩 여부를 검사해 주므로 사용하는 것을 추천한다.
<!-- The "@Override" annotation is not mandatory, but it is recommended to use it because it helps to check the actual overriding during the compile time. -->

```java
// Overriding 예시
class Animal {
    // 상위 클래스의 메서드
    public void makeSound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    // 하위 클래스에서 메서드를 재정의 (오버라이딩)
    @Override
    public void makeSound() {
        System.out.println("Dog barks");
    }
}

class Cat extends Animal {
    // 하위 클래스에서 메서드를 재정의 (오버라이딩)
    @Override
    public void makeSound() {
        System.out.println("Cat meows");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal myDog = new Dog();
        Animal myCat = new Cat();

        myDog.makeSound(); // Dog barks
        myCat.makeSound(); // Cat meows
    }
}
```

## 요약

- Overloading - 같은 클래스 내부에서 이름이 같은 메서드가 다른 시그니처를 가지고 있는 것
<!-- Overloading - methods within the same class having the same name but different signatures. -->

- Overriding - 상속관계의 하위 클래스가 상위 클래스의 이름과 시그니처가 같은 메서드를 재정의 하는 것
<!-- Overriding - When a subclass in an inheritance relationship redefines a method with the same name and signature as that in the superclass. -->
