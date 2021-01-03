# Lesson2 _ Arrays _ CyclicRotation

## 문제

An array A consisting of N integers is given. Rotation of the array means that each element is shifted right by one index, and the last element of the array is moved to the first place. For example, the rotation of array A = [3, 8, 9, 7, 6] is [6, 3, 8, 9, 7] (elements are shifted right by one index and 6 is moved to the first place).

The goal is to rotate array A K times; that is, each element of A will be shifted to the right K times.

Write a function:

class Solution { public int[] solution(int[] A, int K); }

that, given an array A consisting of N integers and an integer K, returns the array A rotated K times.

For example, given

    A = [3, 8, 9, 7, 6]
    K = 3
the function should return [9, 7, 6, 3, 8]. Three rotations were made:

    [3, 8, 9, 7, 6] -> [6, 3, 8, 9, 7]
    [6, 3, 8, 9, 7] -> [7, 6, 3, 8, 9]
    [7, 6, 3, 8, 9] -> [9, 7, 6, 3, 8]
For another example, given

    A = [0, 0, 0]
    K = 1
the function should return [0, 0, 0]

Given

    A = [1, 2, 3, 4]
    K = 4
the function should return [1, 2, 3, 4]

Assume that:

N and K are integers within the range [0..100];
each element of array A is an integer within the range [−1,000..1,000].
In your solution, focus on correctness. The performance of your solution will not be the focus of the assessment.

## 답

- Try 5 : 100%

    ```java
    class Solution {
        public int[] solution(int[] A, int K) {
            int N = A.length;
            int[] shiftRightArray = new int[N];
            
            for(int i=0; i<N; i++){
                shiftRightArray[(i+K)%N] = A[i];
            }

            return shiftRightArray;
        }
    }
    ```

- Try 4 : 37% : 멍청한듯

    ```java
    class Solution {
        public int[] solution(int[] A, int K) {
            // 시작할 index값
            int startIndex = 0;
            int N = A.length;
            
            //N이 0이면 배열 x
            if(N <= 1) return A;

            //N과 K 비교
            if(K < N){
                if(N == 2){
                    startIndex = K;
                }else{
                    startIndex = K-1;
                }
            }else{
                startIndex = K%N;
            }

            // 배열의 index값
            int tempIndex = 0;

            int[] B = new int[A.length];

            for(int i = startIndex; i < B.length; i++){
                B[tempIndex] = A[i];
                tempIndex++;
            }

            for(int i = 0; i<startIndex; i++){
                B[tempIndex] = A[i];
                tempIndex++;
            }

            return B;
        }
    }
    ```

- Try 3 : 25%

    ```java
    class Solution {
        public int[] solution(int[] A, int K) {
           // 시작할 index값
            int startIndex = 0;
            int N = A.length;
            
            //N이 0이면 배열 x
            if(N <= 1) return A;

            //N과 K 비교
            if(K < N){
                startIndex = K-1;
            }else{
                startIndex = K%N;
            }

            // 배열의 index값
            int tempIndex = 0;

            int[] B = new int[A.length];

            for(int i = startIndex; i < B.length; i++){
                B[tempIndex] = A[i];
                tempIndex++;
            }

            for(int i = 0; i<startIndex; i++){
                B[tempIndex] = A[i];
                tempIndex++;
            }

            return B;
        }
    }
    ```

- Try 2 : 0%

    ```java
    class Solution {
        public int[] solution(int[] A, int K) {
             // 시작할 index값
            int startIndex;

            int lengthA = A.length;
            if(K < lengthA){
                startIndex = K-1;
            }else if(K == lengthA || K%lengthA == 0){
                startIndex = 0;
            }else{
                startIndex = K%lengthA;
            }

            // 배열의 index값
            int tempIndex = 0;

            int[] B = new int[A.length];

            for(int i = startIndex; i < B.length; i++){
                B[tempIndex] = A[i];
                tempIndex++;
            }

            for(int i = 0; i<startIndex; i++){
                B[tempIndex] = A[i];
                tempIndex++;
            }

            return B;
        }
    }
    ```

- Try 1 : 12%

    ```java
    class Solution {
        public int[] solution(int[] A, int K) {
            // 시작할 index값
            int startIndex = (K == A.length) ? 0 : K-1;

            // 배열의 index값
            int tempIndex = 0;

            int[] B = new int[A.length];

            for(int i = startIndex; i < B.length; i++){
                B[tempIndex] = A[i];
                tempIndex++;
            }

            for(int i = 0; i<startIndex; i++){
                B[tempIndex] = A[i];
                tempIndex++;
            }

            return B;
        }
    }
    ```

![Lesson2%20_%20Arrays%20_%20CyclicRotation%209570ea1f915248f58b53f0eeb20c0fa7/Untitled.png](Lesson2%20_%20Arrays%20_%20CyclicRotation%209570ea1f915248f58b53f0eeb20c0fa7/Untitled.png)