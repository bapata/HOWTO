# Introduction
  As a devops engineer, one has to maintain code developed in several programming (dynamic scripting) languages. 
I always wanted to write something like – how do I do this in perl/python/ruby (and may be bash/awk/sed/grep) kind of blog and here it is.

Here are some of the initial topics. I won’t claim the code shown here is the most efficient way to do but just one
of the ways to do stuff.

```
#!/usr/bin/{perl, python,ruby} (as appropriate) assumed for each line of code below.
```

## ARGC/ARGV

Invoke script as:
```
script.{pl,py,rb}   myfile.txt

For example, the perl version of the script can be invoked as 
./script.pl myfile.txt

```

### Perl
```
my ($arg1) = @ARGV;
print "Script name: " . __FILE__;
print "\nArgument-1: " . $arg1;
print "\n";
```
### Python
```
import sys
my_script_name,arg1 = sys.argv
print "Script name: " + my_script_name
print "Argument-1: " + arg1
```

### Ruby
```
arg1, = ARGV
puts "Script name: " + __FILE__
puts "Argument-1: " + arg1
```


## Reading contents of a file and storing in a array
Assumption is that we will invoke it as:
```
read_file.{pl,py,rb} myfile.txt
```

### Perl
```
my ($filename) = $ARGV[0];
open(FH,"$filename") || die("Cannot open file: $filename")
my @array = <FH>; # Read entire file contents 
# Verify contents 
print @array
```

### Python
```
import sys
filename = sys.argv[1]
f = open(filename,'r')
array = [ x.rstrip() for x in f.readlines() ] # Get rid of newlines 
print array
```

### Ruby
```
require 'pp' # Pretty print
filename, = ARGV # Get filename
contents = File.readlines(filename)
array = contents.each { |line| line.chomp!() } # modify in place
pp array # Pretty print contents of array
```

 

## Reading a CSV file and generating a hash

### Perl

### Python

### Ruby

 

## Printing a hash as a YAML

### Perl

### Python

### Ruby

 

## Printing hash as a JSON

### Perl

### Python

### Ruby

 

## Report Generator template

### Perl

### Python

### Ruby

 


