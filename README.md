import java.util.Scanner;

abstract class BankAccount {
 double balance;
 BankAccount(double b) { balance = b; }
 void deposit(double a) { if (a > 0) balance += a; }
 abstract void withdraw(double a);
 double getBalance() { return balance; }
}

class SavingsAccount extends BankAccount {
 SavingsAccount(double b) { super(b); }
 void withdraw(double a) {
  if (a > 500) System.out.println("Limit exceeded!");
  else if (a <= balance) balance -= a;
  else System.out.println("Insufficient!");
 }
}

class CurrentAccount extends BankAccount {
 CurrentAccount(double b) { super(b); }
 void withdraw(double a) { balance -= a; }
}

interface Payable { double calculateSalary(); }

class FullTimeEmployee implements Payable {
 double salary;
 FullTimeEmployee(double s) { salary = s; }
 public double calculateSalary() { return salary; }
}

class ContractEmployee implements Payable {
 int hours; double rate;
 ContractEmployee(int h, double r) { hours = h; rate = r; }
 public double calculateSalary() { return hours * rate; }
}

public class Main {
 public static void main(String[] args) {
  Scanner sc = new Scanner(System.in);
  System.out.println("1.Savings 2.Current");
  BankAccount acc = (sc.nextInt() == 1) ? new SavingsAccount(sc.nextDouble()) : new CurrentAccount(sc.nextDouble());
  acc.deposit(sc.nextDouble()); acc.withdraw(sc.nextDouble());
  System.out.println("Balance: $" + acc.getBalance());

  System.out.println("1.FullTime 2.Contract");
  Payable emp = (sc.nextInt() == 1) ? new FullTimeEmployee(sc.nextDouble()) : new ContractEmployee(sc.nextInt(), sc.nextDouble());
  System.out.println("Salary: $" + emp.calculateSalary());
  sc.close();
 }
}
