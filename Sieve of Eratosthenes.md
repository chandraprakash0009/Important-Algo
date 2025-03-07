## Sieve of Eratosthenes

The sieve of Eratosthenes is one of the most efficient ways to find all primes smaller than n when n is smaller than 10 million or so.  
Following is the algorithm to find all the prime numbers less than or equal to a given integer n by the Eratosthenes method:   
When the algorithm terminates, all the numbers in the list that are not marked are prime.

### Java code - 

```
// Java program to print all primes smaller than or equal to
// n using Sieve of Eratosthenes

class SieveOfEratosthenes {
    void sieveOfEratosthenes(int n)
    {
        // Create a boolean array "prime[0..n]" and
        // initialize all entries it as true. A value in
        // prime[i] will finally be false if i is Not a
        // prime, else true.
        boolean prime[] = new boolean[n + 1];
        for (int i = 0; i <= n; i++)
            prime[i] = true;
        // in below loop, "p" is a number which will be checked wither it is prime or not.
        for (int p = 2; p * p <= n; p++) {
            // If prime[p] is not changed, then it is a
            // prime
            if (prime[p] == true) {
                // Update all multiples of p greater than or
                // equal to the square of it numbers which
                // are multiple of p and are less than p^2
                // are already been marked.
                for (int i = p * p; i <= n; i += p)
                    prime[i] = false;
            }
        }

        // Print all prime numbers
        for (int i = 2; i <= n; i++) {
            if (prime[i] == true)
                System.out.print(i + " ");
        }
    }

    // Driver Code
    public static void main(String args[])
    {
        int n = 30;
        System.out.print("Following are the prime numbers ");
        System.out.println("smaller than or equal to " + n);
        SieveOfEratosthenes g = new SieveOfEratosthenes();
        g.sieveOfEratosthenes(n);
    }
}
```

### 2nd Approach - 

Since, we know that prime number starts wwith 2.
Now, think that, if a number "n" is prime then all multiple of "n" except itself will be non-prime. hence mark all its miltiple as non-prime which are less than or equal to given number.  

After applying this algorithm on all element, iterate over boolean array -   
if ith term is true then it is prime otherwise non-prime.

### Java code - 

```

import java.util.*;
public class Main
{
	public static void main(String[] args) {
		int n=200;
		boolean prime[]=new boolean[n+1];
		Arrays.fill(prime,true);  // initially consider all element is prime
		prime[0]=prime[1]=false; // since prime starts with 2
		for(int i=2; i<=n; i++){
		    if(prime[i]){
		        // since "i" is prime, so all multiple of i which are less than or equal to n will be non-prime. Hence mark all its multiple as false(non-prime)
		        for(int j=2; i*j<=n; j++){ // here "i" is the number and "j" is its multiple
		            prime[i*j]=false;
		        }
		    }
		}
		for(int i=0; i<=n; i++){
		    if(prime[i]){
		        System.out.print(i+" ");
		    }
		}
		
	}
}
