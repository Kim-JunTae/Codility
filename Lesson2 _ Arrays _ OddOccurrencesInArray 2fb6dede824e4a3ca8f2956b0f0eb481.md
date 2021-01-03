# Lesson2 _ Arrays _ OddOccurrencesInArray

## 문제

A non-empty array A consisting of N integers is given. The array contains an odd number of elements, and each element of the array can be paired with another element that has the same value, except for one element that is left unpaired.

For example, in array A such that:

  A[0] = 9  A[1] = 3  A[2] = 9
  A[3] = 3  A[4] = 9  A[5] = 7
  A[6] = 9
the elements at indexes 0 and 2 have value 9,
the elements at indexes 1 and 3 have value 3,
the elements at indexes 4 and 6 have value 9,
the element at index 5 has value 7 and is unpaired.
Write a function:

class Solution { public int solution(int[] A); }

that, given an array A consisting of N integers fulfilling the above conditions, returns the value of the unpaired element.

For example, given array A such that:

  A[0] = 9  A[1] = 3  A[2] = 9
  A[3] = 3  A[4] = 9  A[5] = 7
  A[6] = 9
the function should return 7, as explained in the example above.

Write an efficient algorithm for the following assumptions:

N is an odd integer within the range [1..1,000,000];
each element of array A is an integer within the range [1..1,000,000,000];
all but one of the values in A occur an even number of times.

## 답

- Try 2 : 66%, Time Complexity

    ```java
    class Solution {
        public int solution(int[] A) {
            int result = 0;

            for(int i=0; i<A.length-1; i++){
                for(int j=i+1; j<A.length; j++){
                    if(A[i] == A[j]){
                        A[i] = 0;
                        A[j] = 0;
                        break;
                    }
                }
            }

            for(int a : A){
                if(a != 0){
                    result = a;
                }
            }

            return result;
        }
    }
    ```

![Lesson2%20_%20Arrays%20_%20OddOccurrencesInArray%202fb6dede824e4a3ca8f2956b0f0eb481/Untitled.png](Lesson2%20_%20Arrays%20_%20OddOccurrencesInArray%202fb6dede824e4a3ca8f2956b0f0eb481/Untitled.png)

- Try 1

    ```java
    // you can also use imports, for example:
    import java.util.*;

    // you can write to stdout for debugging purposes, e.g.
    // System.out.println("this is a debug message");

    class Solution {
        public int solution(int[] A) {
            //List vs Set
            Set<Map<Integer, Integer>> numberList = new HashSet<Map<Integer, Integer>>();
            
            //존재하는 
            for(int i=0; i<A.length; i++){
                Map<Integer, Integer> numberMap = new HashMap<Integer, Integer>();
                int number = A[i];
                numberMap.put(number, 0);
                numberList.add(numberMap);
            }
            
            for(int i=0; i<A.length; i++){
                int number = A[i];
                for(Map<Integer, Integer> map : numberList){
                    if(map.get(number) != null){
                        int count = map.get(number);
                        map.put(number, count++);
                    }
                }
            }

            for(int i=0; i<A.length; i++){
                int number = A[i];
                for(Map<Integer, Integer> map : numberList){
                    if(map.get(number) != null){
                        int count = map.get(number);
                        if(count%2 != 0){
                            return number;
                        }
                    }
                }
            }

            return -1;
        }
    }
    ```