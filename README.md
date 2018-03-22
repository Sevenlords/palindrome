# palindrome
Find the largest palindrome made from the product of two 5-digit prime numbers

public class Main {

    private static ArrayList<Integer> primeList = new ArrayList<>();
    private static ArrayList<Integer> bigPrimeList = new ArrayList<>();
    private static String palindromeStr = "0";
    private static long palindromeMax = 0;

    private static void initPrimeList() {
        primeList.add(2);
        for (int i = 3; i < 100000; i++) {
            setPrimeList(i);
        }
    }

    private static void setPrimeList(int num) {
        int i = 0;
        boolean bool = false;

        while (num % primeList.get(i) != 0) {
            bool = true;
            i++;
            if (i == primeList.size()) {
                i--;
                break;
            }
        }

        if (num % primeList.get(i) == 0) bool = false;

        if (bool) {
            primeList.add(num);
            if (num > 10000) {
                bigPrimeList.add(num);
            }
        }
    }

    private static void maxPalindrome(ArrayList<Integer> l) {
        for (int i = 0; i < l.size(); i++) {
            for (int m = i + 1; m < l.size(); m++) {
                long amount = (long) l.get(i) * l.get(m);
                Palindrome(amount,l.get(i),l.get(m));
            }
        }
    }

    private static void Palindrome(long am, int i, int m) {
        String string = String.valueOf(am);
        boolean bool = false;

        for (int step = 0; step <= string.length() / 2; step++) {
            if (string.charAt(step) != string.charAt(string.length() - step - 1)) {
                bool = false;
                break;
            } else bool = true;
        }
        if (bool) {
            if (am > palindromeMax) {
                palindromeMax = am;
                palindromeStr = string.concat("=" + i + "*" + m);
            }
        }
    }

    public static void main(String[] args) {

        initPrimeList();

        maxPalindrome(bigPrimeList);

        System.out.println(palindromeStr);

    }
}
