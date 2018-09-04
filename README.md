A perfect number is a positive integer that is equal to the sum of its proper positive divisors, 
that is, the sum of its positive divisors excluding the number itself.

See http://en.wikipedia.org/wiki/Perfect_number
If the sum of proper positive divisors is less than the number then we'll call it "deficient". 
If it is greater - the number will be called "abundant". 
The task is to create a PerfectNumber.detect(int n) method, which for a given positive integer will return it's classification: deficient, perfect or abundant.

First, in order to understand task and debug the algorithm, create an imperative solution consisting of divisor list generator 
public static Set<Integer> divisors(int n)
and number classifier
public static STATE process(int n)
using the tests below to verify both.

Then rework it to employ Java 8 lambdas and streams. 
The functional solution shall ideally feature no if's, while's and for's.

After you have a nice functional solution, try to add a subtle yet powerful optimization - reduce divisor checking range to
1..Math.sqrt ( n )

Here are some tests one can use to check the divisor generator in the imperative solution:

```java
@Test
public void testDivisors1() {
Object[] expected = new Integer[] { 1 };
int n = 1;
assertArrayEquals(expected, PerfectNumber.divisors( n ).toArray());
}
@Test
public void testDivisors6() {
Object[] expected = new Integer[] { 1, 2, 3, 6 };
int n = 6;
assertArrayEquals(expected, PerfectNumber.divisors( n ).toArray());
}
@Test
public void testDivisors8() {
Object[] expected = new Integer[] { 1, 2, 4, 8 };
int n = 8;
assertArrayEquals(expected, PerfectNumber.divisors( n ).toArray());
}
```

The following tests can be use to test both imperative and functional solution:

```java
import static org.junit.Assert.assertEquals;
import static retreat.PerfectNumber.STATE.ABUNDANT;
import static retreat.PerfectNumber.STATE.DEFICIENT;
import static retreat.PerfectNumber.STATE.PERFECT;
import org.junit.Test;
public class PerfectNumberTest {
@Test
public void test6Perfect() {
assertEquals(PERFECT, PerfectNumber.process(6));
}
@Test
public void test8Deficient() {
assertEquals(DEFICIENT, PerfectNumber.process(8));
}
@Test
public void test20Abundant() {
assertEquals(ABUNDANT, PerfectNumber.process(20));
}
@Test
public void test16DeficientWithIntSqrt() {
assertEquals(DEFICIENT, PerfectNumber.process(16));
}
@Test
public void test1Deficient() {
assertEquals(DEFICIENT, PerfectNumber.process(1));
}

}
```
