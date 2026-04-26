//1-Rahul is analyzing
// Maximum Subarray Sum - Kadane's Algorithm
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();
        int[] arr = new int[n];

        for (int i = 0; i < n; i++) {
            arr[i] = sc.nextInt();
        }

        int maxSum = arr[0];
        int currentSum = arr[0];

        for (int i = 1; i < n; i++) {
            currentSum = Math.max(arr[i], currentSum + arr[i]);
            maxSum = Math.max(maxSum, currentSum);
        }

        System.out.print(maxSum);
    }
}




//2-Sanjay is working 

// Merge Two Sorted LinkedLists
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int m = sc.nextInt();
        LinkedList<Integer> list1 = new LinkedList<>();
        for (int i = 0; i < m; i++) {
            list1.add(sc.nextInt());
        }

        int n = sc.nextInt();
        LinkedList<Integer> list2 = new LinkedList<>();
        for (int i = 0; i < n; i++) {
            list2.add(sc.nextInt());
        }

        LinkedList<Integer> result = new LinkedList<>();

        int i = 0, j = 0;

        while (i < list1.size() && j < list2.size()) {
            if (list1.get(i) <= list2.get(j)) {
                result.add(list1.get(i));
                i++;
            } else {
                result.add(list2.get(j));
                j++;
            }
        }

        while (i < list1.size()) {
            result.add(list1.get(i));
            i++;
        }

        while (j < list2.size()) {
            result.add(list2.get(j));
            j++;
        }

        for (int val : result) {
            System.out.print(val + " ");
        }
    }
}



//3-In the city of Luthonia,

// Maximum Brightness Substring - Modified Kadane's Algorithm
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String s = sc.nextLine();

        int maxSum = Integer.MIN_VALUE;
        int currentSum = 0;
        int start = 0, end = 0, tempStart = 0;

        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            int value;

            if (c >= 'a' && c <= 'z') {
                value = c - 'a' + 1;
            } else {
                value = -(c - 'A' + 1);
            }

            if (currentSum + value < value) {
                currentSum = value;
                tempStart = i;
            } else {
                currentSum += value;
            }

            if (currentSum > maxSum) {
                maxSum = currentSum;
                start = tempStart;
                end = i;
            }
        }

        System.out.println(maxSum);
        System.out.println(s.substring(start, end + 1));
    }
}



//4-Assist Pranitha

// Count Frequency of a Name in ArrayList
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();
        sc.nextLine();

        ArrayList<String> list = new ArrayList<>();

        for (int i = 0; i < n; i++) {
            list.add(sc.nextLine());
        }

        String search = sc.nextLine();
        int count = 0;

        for (String name : list) {
            if (name.equals(search)) {
                count++;
            }
        }

        System.out.print(count);
    }
}




//5-Riya is working
// Find First Occurrence of Pattern in Text - KMP Algorithm
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        String text = sc.nextLine();
        String pattern = sc.nextLine();

        int[] lps = computeLPS(pattern);

        int i = 0, j = 0;

        while (i < text.length()) {
            if (text.charAt(i) == pattern.charAt(j)) {
                i++;
                j++;
            }

            if (j == pattern.length()) {
                System.out.print(i - j);
                return;
            } else if (i < text.length() && text.charAt(i) != pattern.charAt(j)) {
                if (j != 0) {
                    j = lps[j - 1];
                } else {
                    i++;
                }
            }
        }

        System.out.print(-1);
    }

    public static int[] computeLPS(String pattern) {
        int[] lps = new int[pattern.length()];
        int len = 0;
        int i = 1;

        while (i < pattern.length()) {
            if (pattern.charAt(i) == pattern.charAt(len)) {
                len++;
                lps[i] = len;
                i++;
            } else {
                if (len != 0) {
                    len = lps[len - 1];
                } else {
                    lps[i] = 0;
                    i++;
                }
            }
        }
        return lps;
    }
}



//6-A city traffic management system need
// Store Unique Vehicle Records using HashSet
import java.util.*;

class Vehicle {
    String regNumber;
    String ownerName;
    String vehicleType;

    Vehicle(String regNumber, String ownerName, String vehicleType) {
        this.regNumber = regNumber;
        this.ownerName = ownerName;
        this.vehicleType = vehicleType;
    }

    public boolean equals(Object o) {
        if (this == o) return true;
        if (!(o instanceof Vehicle)) return false;
        Vehicle v = (Vehicle) o;
        return regNumber.equals(v.regNumber);
    }

    public int hashCode() {
        return regNumber.hashCode();
    }

    public String toString() {
        return regNumber + " " + ownerName + " " + vehicleType;
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();
        sc.nextLine();

        HashSet<Vehicle> set = new HashSet<>();

        for (int i = 0; i < n; i++) {
            String line = sc.nextLine();
            String[] parts = line.split(" ");
            set.add(new Vehicle(parts[0], parts[1], parts[2]));
        }

        for (Vehicle v : set) {
            System.out.println(v);
        }
    }
}



//7-Sophia is a librarian who 

```java id="b9m4q"
// Boyer-Moore String Search (Bad Character Heuristic)
import java.util.*;

public class Main {

    static int[] badCharTable(String pat) {
        int[] badChar = new int[256];
        Arrays.fill(badChar, -1);

        for (int i = 0; i < pat.length(); i++) {
            badChar[pat.charAt(i)] = i;
        }
        return badChar;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        String text = sc.nextLine();
        String pattern = sc.nextLine();

        int[] badChar = badCharTable(pattern);

        int n = text.length();
        int m = pattern.length();

        boolean found = false;
        int shift = 0;

        while (shift <= (n - m)) {
            int j = m - 1;

            while (j >= 0 && pattern.charAt(j) == text.charAt(shift + j)) {
                j--;
            }

            if (j < 0) {
                System.out.println(shift);
                found = true;

                shift += (shift + m < n) ? m - badChar[text.charAt(shift + m)] : 1;
            } else {
                shift += Math.max(1, j - badChar[text.charAt(shift + j)]);
            }
        }
    }
}
```



//8-John is organizing a fruit festival
// Sum of Fruit Quantities using HashMap
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        HashMap<String, Double> map = new HashMap<>();
        double sum = 0.0;

        while (true) {
            String input = sc.nextLine();

            if (input.equalsIgnoreCase("done")) break;

            int colonCount = 0;
            for (char c : input.toCharArray()) {
                if (c == ':') colonCount++;
                else if (!Character.isLetter(c) && c != '.' && !Character.isDigit(c)) {
                    System.out.print("Invalid format");
                    return;
                }
            }

            if (colonCount != 1) {
                System.out.print("Invalid format");
                return;
            }

            String[] parts = input.split(":");
            String fruit = parts[0];
            String value = parts[1];

            double quantity;
            try {
                quantity = Double.parseDouble(value);
            } catch (Exception e) {
                System.out.print("Invalid input");
                return;
            }

            map.put(fruit, quantity);
        }

        for (double val : map.values()) {
            sum += val;
        }

        System.out.printf("%.2f", sum);
    }
}


//9-﻿In a futuristic city
// Longest Palindromic Substring
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String s = sc.nextLine().toLowerCase();

        int start = 0, maxLen = 1;

        for (int i = 0; i < s.length(); i++) {
            int l = i, r = i;
            while (l >= 0 && r < s.length() && s.charAt(l) == s.charAt(r)) {
                if (r - l + 1 > maxLen) {
                    start = l;
                    maxLen = r - l + 1;
                }
                l--;
                r++;
            }

            l = i;
            r = i + 1;
            while (l >= 0 && r < s.length() && s.charAt(l) == s.charAt(r)) {
                if (r - l + 1 > maxLen) {
                    start = l;
                    maxLen = r - l + 1;
                }
                l--;
                r++;
            }
        }

        System.out.print(s.substring(start, start + maxLen));
    }
}


//10-Dinu is building
// Word Frequency using HashMap (Maintain Insertion Order)
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String line = sc.nextLine();

        String[] words = line.split(" ");
        LinkedHashMap<String, Integer> map = new LinkedHashMap<>();

        for (String word : words) {
            map.put(word, map.getOrDefault(word, 0) + 1);
        }

        for (Map.Entry<String, Integer> entry : map.entrySet()) {
            System.out.println(entry.getKey() + " : " + entry.getValue());
        }
    }
}
