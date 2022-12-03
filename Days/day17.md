On the seventeenth day, I learned the following things about YAML.

## Write a sequence

    ---
    student: !!seq
    - mark
    - name
    - roll_no
    ...

## Empty sequence will be called sparse sequence

    ---
    sparse seq:
    - how
    - where
    - 
    - Null
    - sup
    ...

## Write a nested sequence

    ---
    -
    - mango
    - orange
    - apple
    - 
    - car
    - truck
    - bus
    ...

## Key value pairs are called maps
    !!map

## Write nested mappings: map within a map
    
    ---
    name: Bilal Khan
    roles:
    age: 12
    job: software engineer
    ...

### **same like this**

    ---
    name: Bilal Khan
    roles: {age: 12, job: software engineer}
    ...

## Write pairs which means that one key may have multiple values

    !!pairs

### **Example**

    ---
    pair example: !!pairs
    - job: student
    - job: teacher
    ...

### **same like this**

    ---
    pair example: !!pairs [job: student, job: teacher]
    ...

### **this will be an array of hashtables**

## Set will allow you to have unique values

    ---
    names: !!set
    ? Bilal
    ? Ali
    ? Ahmed
    ...

## Write a dictionary that will represent sequence as a value

    !!omap

### **Example**

    ---
    people:
    - Bilal:
        name: Bilal Khan
        age: 25
        role: software engineer
    - Ali:
        name: Ali Ahmed
        age: 19
        role: data scientist
    ...

## Re-use some properties using anchors

    likings: &fruitsChoice
    like: mango
    dislike: banana

    person1:
    name: Bilal
    <<: *fruitsChoice

    person2:
    name: Hamza
    <<: *fruitsChoice

    person3:
    name: Ali
    <<: *fruitsChoice

### **Result**

    person1:
    name: Bilal
    like: mango
    dislike: banana

## If you want to override some data. The data will be replaced with a new one

    person1:
    name: Bilal
    like: mango
    <<: *fruitsChoice
    dislike: orange

### **Result**

    person1:
    name: Bilal
    like: mango
    dislike: orange

## Example of multiple nested sequence

    Schools:
    - name: DPS
        principal: Someone
        students:
        - roll_no: 12
            name: Bilal Khan
            marks: 5

## **Explaining it in a video**

Here you can get an explanation in a video. [17/60 Day of DevOps Challenge](https://www.youtube.com/watch?v=fW57FPJnAcg&list=PLptbpfKzsc3BtEki4tHQm5Xmpj8w1_JlM&index=16)