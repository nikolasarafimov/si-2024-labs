# 🧪 Software Engineering – Lab Exercise 2  
**Course:** Software Engineering  
**Author:** Nikola Sarafimov (223091)  
**Academic Year:** 2023/2024 

## (1) Control Flow Graph:

![CFG drawio](https://github.com/nikolasarafimov/SI_2024_lab2_223091/assets/134642898/1b1d0057-5eda-48d6-aa4a-61d6c26860ce)

## (2) Cyclomatic Complexity:
Cyclomatic complexity of this code = E (number of edges) – N (number of nodes) + 2 => 36 − 28 + 2 = 10

## (3) Test cases according to the Every Branch criterion
Test case 1: allItems is null

     - Input: checkCart(null, 100)
     - Expected output: RuntimeException with message "allItems list can't be null!"
     - Covered branches: 1, 2

Test case 2: allItems is empty

     - Input: checkCart(Collections.emptyList(), 100)
     - Expected output: true
     - Covered branches: 3, 21, 22

Test case 3: item with null name

     - Input: checkCart(List.of(new Item(null, "123", 100, 0)), 100)
     - Expected output: true
     - Covered branches: 3, 4.1, 4.2, 4.3, 5, 6, 7, 8, 9, 10.1, 10.2, 10.3, 11, 12, 14, 16, 17, 21, 22

Test case 4: item with invalid barcode character

     - Input: checkCart(List.of(new Item("item1", "12a", 100, 0)), 100)
     - Expected output: RuntimeException with message "Invalid character in item barcode!"
     - Covered branches: 3, 4.1, 4.2, 4.3, 5, 6, 8, 9, 10.1, 10.2, 10.3, 11, 12, 13

Test case 5: item with null barcode

     - Input: checkCart(List.of(new Item("item1", null, 100, 0)), 100)
     - Expected output: RuntimeException with message "No barcode!"
     - Covered branches: 3, 4.1, 4.2, 4.3, 5, 6, 8, 18

Test case 6: item with discount > 0

     - Input: checkCart(List.of(new Item("item1", "123", 100, 0.1f)), 100)
     - Expected output: true
     - Covered branches: 3, 4.1, 4.2, 4.3, 5, 6, 8, 9, 10.1, 10.2, 10.3, 11, 12, 14, 15, 17, 21, 22

Test case 7: item with price > 300, discount > 0, barcode starting with '0'

     - Input: checkCart(List.of(new Item("item1", "0123", 400, 0.1f)), 100)
     - Expected output: true
     - Covered branches: 3, 4.1, 4.2, 4.3, 5, 6, 8, 9, 10.1, 10.2, 10.3, 11, 12, 14, 15, 17, 19, 20, 21, 22

Test case 8: sum > payment

     - Input: checkCart(List.of(new Item("item1", "123", 200, 0)), 100)
     - Expected output: false
     - Covered branches: 3, 4.1, 4.2, 4.3, 5, 6, 8, 9, 10.1, 10.2, 10.3, 11, 12, 14, 16, 17, 21, 23

## (4) Test cases according to the Multiple Condition criterion
The condition if (item.getPrice() > 300 && item.getDiscount() > 0 && item.getBarcode().charAt(0) == '0') includes three sub-conditions:

     item.getPrice() > 300 (Услов A)
     item.getDiscount() > 0 (Услов B)
     item.getBarcode().charAt(0) == '0' (Услов C)
Each condition has two possible values: true (T) or false (F). Therefore, all combinations must be tested, giving 2³ = 8 test cases.

Test case 1: A = T, B = T, C = T

     - Input: checkCart(List.of(new Item("item1", "0123", 400, 0.1f)), 100)
     - Expected output: true
     - Explanation: All conditions are true; price > 300, discount > 0, barcode starts with '0'. Sum will be reduced by 30.

Test case 2: A = T, B = T, C = F

     - Input: checkCart(List.of(new Item("item1", "1123", 400, 0.1f)), 100)
     - Expected output: false
     - Explanation: Only the barcode condition is false (does not start with '0'). Sum will not be reduced by 30.

Test case 3: A = T, B = F, C = T

     - Input: checkCart(List.of(new Item("item1", "0123", 400, 0)), 100)
     - Expected output: false
     - Explanation: Only the discount condition is false (discount is 0). Sum will not be reduced by 30.

Test case 4: A = T, B = F, C = F

     - Input: checkCart(List.of(new Item("item1", "1123", 400, 0)), 100)
     - Expected output: false
     - Explanation: Both discount and barcode conditions are false. Sum will not be reduced by 30.

Test case 5: A = F, B = T, C = T

     - Input: checkCart(List.of(new Item("item1", "0123", 200, 0.1f)), 100)
     - Expected output: true
     - Explanation: Only the price condition is false (price ≤ 300). Sum will not be reduced by 30.

Test case 6: A = F, B = T, C = F

     - Input: checkCart(List.of(new Item("item1", "1123", 200, 0.1f)), 100)
     - Expected output: true
     - Explanation: Price and barcode conditions are false. Sum will not be reduced by 30.

Test case 7: A = F, B = F, C = T

     - Input: checkCart(List.of(new Item("item1", "0123", 200, 0)), 100)
     - Expected output: true
     - Explanation: Price and discount conditions are false. Sum will not be reduced by 30.

Test case 8: A = F, B = F, C = F

     - Input: checkCart(List.of(new Item("item1", "1123", 200, 0)), 100)
     - Expected output: true
     - Explanation: All conditions are false. Sum will not be reduced by 30.
