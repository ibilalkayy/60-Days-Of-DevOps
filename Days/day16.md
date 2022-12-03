On the sixteenth day, I learned the following things about YAML.

## Starting and ending point

    '---' is the starting point
    '...' is an ending point

**Note: YAML doesn't support multi-line comment. It only supports '#' to be written with each line like this**

    # This is the first line
    # This is the second line
    # This is the third line

## Write key value pair
    
**Syntax:** ***key: value***

    ---
    name: Bilal Khan
    1: This is a number
    {fruit: mango, age: 12}
    ...

## Write a list
    ---
    - apple
    - mango
    - orange
    - Apple
    ...

## Write data in block style

    ---
    cities:
    - city1
    - city2
    - city3

    cities: [city1, city2, city3]
    ...

## String values
**YAML provide 3 types of string values**

    ---
    name: Bilal Khan
    fruit: "this is a mango"
    job: 'software engineering'
    ...

## Write data in separate lines by inserting '|' sign
    ---
    bio: |
    "My name is Bilal"
    "I am a developer"
    ...

## Write single line in multiple lines by inserting '>' sign

    ---
    message: > 
    this is a single
    line that I am
    writing in multiple
    lines
    ...

## YAML will automatically detect the data type

    ---
    number: 43
    float: 34.65
    boolean: Y # y, true, True, n, N, false, False
    ...

## Write data types
**Integer data type**

    ---
    zero: !!int 0
    positiveNum: !!int 54
    negativeNum: !!int -54
    binaryNum: !!int 0b1011
    octalNum: !!int 05346
    hexaDecNum: !!int 0x54
    commaVal: !!int 25_000 # is equal to 25,000
    exponentialVal: !!int 6.02E54
    ...

**Float data type**

    ---
    marks: !!float 54.65
    infinite: !!float .inf
    not a num: .nan
    ...

**String and boolean data type**

    ---
    string: !!str "this is a string"
    ---
    boolean: !!bool True
    ...

**Null data type**

    ---
    null: !!null Null # !!null Null ~
    ~: this is also a key
    ...

**Date data type**

    ---
    date: !!timestamp 2002-12-14
    pakistan time: 2001-12-15T02:59:43.10 + 8:13
    not a time zone: 2001-12-15T02:59:43.1Z
    ...

## **Explaining it in a video**

Here you can get an explanation in a video. [16/60 Day of DevOps Challenge](https://www.youtube.com/watch?v=XYnOY6slAdQ&list=PLptbpfKzsc3BtEki4tHQm5Xmpj8w1_JlM&index=15)