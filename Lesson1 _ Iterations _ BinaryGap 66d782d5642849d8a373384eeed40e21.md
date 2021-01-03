# Lesson1 _ Iterations _ BinaryGap

## 문제

A binary gap within a positive integer N is any maximal sequence of consecutive zeros that is surrounded by ones at both ends in the binary representation of N.

For example, number 9 has binary representation 1001 and contains a binary gap of length 2. The number 529 has binary representation 1000010001 and contains two binary gaps: one of length 4 and one of length 3. The number 20 has binary representation 10100 and contains one binary gap of length 1. The number 15 has binary representation 1111 and has no binary gaps. The number 32 has binary representation 100000 and has no binary gaps.

Write a function:

class Solution { public int solution(int N); }

that, given a positive integer N, returns the length of its longest binary gap. The function should return 0 if N doesn't contain a binary gap.

For example, given N = 1041 the function should return 5, because N has binary representation 10000010001 and so its longest binary gap is of length 5. Given N = 32 the function should return 0, because N has binary representation '100000' and thus no binary gaps.

Write an efficient algorithm for the following assumptions:

N is an integer within the range [1..2,147,483,647].

## 답

```java
6%
class Solution {
    public int solution(int N) {
        String binary = Integer.toBinaryString(N);
        int response = 0;
        int temp = 0;

        if(binary.charAt(binary.length()-1) == '0'){
            return 0;
        }

        for(int i=1; i<binary.length()-1; i++){
            if(binary.charAt(i) == '0'){
                temp++;
            }else{  // 1 일때 
                if(response < temp){
                    response = temp;
                    temp = 0;
                }else{
                    temp = 0;
                }
            }
        }

        return response;
    }
}
```

```java
33%
class Solution {
    public int solution(int N) {
        String binaryN = Integer.toBinaryString(N);
        int binaryNLength = binaryN.length();

        int response = 0;
        int temp = 0;

        if(binaryN.lastIndexOf("1") == 0){
            return 0;
        }

        for(int i=1; i<binaryNLength; i++){
            if(binaryN.substring(i-1, i).equals("0")){
                temp++;
            }else{
                if(temp > response){
                    response = temp;
                }

                temp = 0;
            }
        }

        return response;
    }
}
```

아뉘 60퍼 어떻게 한거여!, 결국 구글링 참고. 너무 쉬운 문제였다.

[https://bono915.tistory.com/entry/코딜리티codility-Lesson1-BinaryGap-문제-풀이JAVA](https://bono915.tistory.com/entry/%EC%BD%94%EB%94%9C%EB%A6%AC%ED%8B%B0codility-Lesson1-BinaryGap-%EB%AC%B8%EC%A0%9C-%ED%92%80%EC%9D%B4JAVA)

```java
class Solution {
    public int solution(int N) {
        // https://bono915.tistory.com/ 참조
        int result = 0;
        int oneCount = 0;
        int zeroCount = 0;
        int topZeroCount = 0;

        String a = Integer.toBinaryString(N);

        for(int i=0; i<a.length(); i++){
            if(a.charAt(i) == '0'){
                zeroCount++;
            }else if(a.charAt(i) == '1'){
                oneCount++;
                if(topZeroCount < zeroCount){
                    topZeroCount = zeroCount;
                }
                zeroCount = 0;
            }
        }

        if(oneCount < 2){
            result = 0;
        }else{
            result = topZeroCount;
        }

        return result;
    }
}
```