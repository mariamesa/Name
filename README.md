# Name
This class reads in names from a file and then prints the name in a few ways, as well as its initials. When the entire file is read, it returns the number of names read in.

import java.util.Scanner;
import java.io.*;

public class Name {
    public Name(String last, String first) {
        this.last = last;
        this.first = first;
    }
    public Name(String first) {this("", first);}
    public String getFormal() {return first + " " + last;}
    public String getOfficial() {return last + ", " + first;}
    public String getInitials () {
        return first.charAt(0) + "." + last.charAt(0) + ".";
    }
    public boolean equals(Name other)  {
        return first.equals(other.first) && last.equals(other.last);}
    public String toString() {return first + " " + last;}
    public static Name read(Scanner scanner) {
        if (!scanner.hasNext()) return null;
        String last = scanner.next();
        String first = scanner.next();
        return new Name(last, first);
    }
    private String first, last, middle;
    public static void main(String [] args) throws Exception {
        Scanner scanner = new Scanner(new File("names.text"));
        int count = 0;
        Name name = read(scanner);
        Name other = null;
        while(name != null) {
           if (other == null || !(name.equals(other))) {
               System.out.println("name: " + name.toString());
               System.out.println("formal: " + name.getFormal());
               System.out.println("official: " + name.getOfficial());
               System.out.println("initials: " + name.getInitials());
               System.out.println();
           }
           else {
               System.out.println("Duplicate name  \""  +  name.toString() + "\" discovered");
           }
            count++;
            other = name;
            name = read(scanner);
        }
        System.out.println("---");
        System.out.println(count + " names processed.");
    }
}
