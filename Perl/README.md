# Perl 5 Cheatsheet

## Table of Contents

- [General](#general)
- [Strings and Numbers 1](#strings-and-numbers-1)
- [Strings and Numbers 2](#strings-and-numbers-2)
- [Subroutines 1](#subroutines-1)

## General

```perl
# Tell the compiler to generate errors if variables are not declared
use strict;

# Tell the compiler to show warnings
use warnings;

# my creates block scoped variables
my $value = 0;

# Print the Perl version
# It prints something like 5.018002, which means 5.18.2
print("$]\n");

# Print the operating sysyem
# It prints something like darwin, linux, MSWin32, etc.
print("$^O\n");
```

References:
- http://www.perlmonks.org/?node_id=185675


## Strings and Numbers 1

```perl
use strict;
use warnings;

my $scalar1 = 8;
my $scalar2 = 42;
my $scalar3 = "8";

# Numeric Comparison:
# ==, !=, <, >, <=, >=, <=>
my $result1 = $scalar1 == $scalar2;   # undef
my $result2 = $scalar1 < $scalar2;    # 1
my $result3 = $scalar1 <=> $scalar2;  # -1

# String Comparison:
# eq, ne, lt, gt, le, ge, cmp
my $result4 = $scalar1 eq $scalar3;   # 1
my $result5 = $scalar1 lt $scalar2;   # undef
my $result6 = $scalar1 cmp $scalar2;  # 1

# Arithmetic Operators
# $scalar3 behaves like a number
print($scalar2 + $scalar3, "\n");   #       Addition: 50
print($scalar2 - $scalar3, "\n");   #    Subtraction: 34
print($scalar2 * $scalar3, "\n");   # Multiplication: 336
print($scalar2 / $scalar3, "\n");   #       Division: 5.25
print($scalar2 % $scalar3, "\n");   #      Remainder: 2
print($scalar2 ** $scalar3, "\n");  # Exponentiation: 9682651996416
print("\n");
print($scalar2++, "\n");            # Post-Increment: 42
print($scalar2, "\n");              #                 43
print(++$scalar2, "\n");            #  Pre-Increment: 44
print("\n");

# String Operators
# $scalar1 behaves like a string
print($scalar1 . $scalar3, "\n");  # Concatenation: 88
print($scalar1 x $scalar3, "\n");  #    Repetition: 88888888
print("\n");

# Single Quotes and Double Quotes
print('$scalar1, $scalar2', "\n");  # $scalar1, $scalar2
print("$scalar1, $scalar2\n");      # 8, 44
```

References:
- `man perlop`

## Strings and Numbers 2

```perl
use strict;
use warnings;

my $scalar1 = 8;
my $scalar4 = "foo";
my $scalar5 = "bar";

# $scalar4 behaves like zero
print($scalar4 + $scalar1, "\n");    # 8, Warning: Argument "foo" isn't numeric in addition (+)
print($scalar4 - $scalar1, "\n");    # -8
print($scalar4 * $scalar1, "\n");    # 0
print($scalar4 / $scalar1, "\n");    # 0
print($scalar4 % $scalar1, "\n");    # 0
print($scalar4 ** $scalar1, "\n");   # 0
print("\n");
print($scalar1 + $scalar4, "\n");    # 8
print($scalar1 - $scalar4, "\n");    # 8
print($scalar1 * $scalar4, "\n");    # 0
# print($scalar1 / $scalar4, "\n");  # Error: Illegal division by zero
# print($scalar1 % $scalar4, "\n");  # Error: Illegal modulus zero
print($scalar1 ** $scalar4, "\n");   # 1
print("\n");

# String Increment
print($scalar5++, "\n");  # Post-Increment: bar
print($scalar5, "\n");    #                 bas
print(++$scalar5, "\n");  #  Pre-Increment: bat
print("\n");

# String Increment (Weird Behaviour)
# $scalar4 becomes a number after the warning above
# Tested on:
# - Perl v5.18.2 on darwin
# - Perl v5.24.2 on linux
print($scalar4++, "\n");  # Post-Increment: foo
print($scalar4, "\n");    #                 1
print(++$scalar4, "\n");  #  Pre-Increment: 2
print("\n");
```

## Subroutines 1

```perl
use strict;
use warnings;

# Subroutine Forward Declaration
sub print_first_three_arguments;

# This prints: Amy Bob Cody
print_first_three_arguments("Amy", "Bob", "Cody", "Dan");

# Parentheses are optional
print_first_three_arguments "Amy", "Bob", "Cody", "Dan";

sub print_first_three_arguments {
    my $first = shift;
    my $second = shift;
    my $third = shift;
    print($first, " ", $second, " ", $third, "\n");
}

# Subroutine Reference (Function Pointer)
my $p3ptr = \&print_first_three_arguments;
$p3ptr->("Amy", "Bob", "Cody", "Dan");

# Old syntax, same result
&$p3ptr("Amy", "Bob", "Cody", "Dan");

# Anonymous Subroutine
my $p3anon = sub {
    my $first = shift;
    my $second = shift;
    my $third = shift;
    print($first, " ", $second, " ", $third, "\n");
};
$p3anon->("Amy", "Bob", "Cody", "Dan");

# Old syntax, same result
&$p3anon("Amy", "Bob", "Cody", "Dan");
```
