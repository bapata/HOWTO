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
These code snippets demonstrate how to read key,value pairs in a hash data structure (aka Map).
If possible, I am avoiding external file as input and using builtin data (__DATA__ (perl) and __END__ in ruby )

### Perl
```
use Data::Dumper;
my %hash;
while(<DATA>) {
  my ($key,$value) = split(/\,/);
  chomp $value;
  $hash{$key} = $value;
}

print Dumper(\%hash);
__DATA__
key1,value1
key2,value2
key3,value3
```

### Python
Python has no easy way to have data in source code. So, I assume that key1,value1 entries are in an external
text file and is passed as a first argument for this script:
```
import sys

hash={}
filename=sys.argv[1] # csv_to_hash.py csvfile.txt
fobj = open(filename,'r')
for line in fobj:
  key,val = line.split(',')
  val=val.rstrip()
  hash[key]=val

print hash
```


### Ruby
```
require 'pp'
hash={}
DATA.each do |line|
  key,val = line.split(/\,/)
  val.chomp!()
  hash[key]=val
end
pp hash

__END__
key1,value1
key2,value2
key3,value3
```
 

## Printing a hash as a YAML
These code snippets will assume that we have a hash (Map) data structure available.

### Perl
```
use YAML;

my %hash = {
  'key1' => 'value1',
  'key2' => 'value2',
  'key3' => 'value3',
};

print Dump(\%hash)
```

### Python

### Ruby
```
require 'yaml'
hash = {
  'key1' => 'value1',
  'key2' => 'value2',
  'key3' => 'value3',
}

puts hash.to_yaml()
```

## Printing hash as a JSON

### Perl



### Python
```
import json

hash = {
  'key1' : 'value1',
  'key2' : 'value2',
  'key3' : 'value3',
}

print json.dumps(hash)
```

### Ruby
```
require 'json'

hash = {
  'key1' => 'value1',
  'key2' => 'value2',
  'key3' => 'value3',
}

puts JSON.generate(hash)
```


 

## Report Generator template

### Perl
```
my $from="from_value";
my $to="To_Value";

my $message = <<'END_MESSAGE';
Dear $from,
  Attached is the report.
    Yours faithfully,
     $to

END_MESSAGE

print $message;
```


### Python
```
message="""
this is the multiline
message in python
"""
print message
```

### Ruby
```
from_var='From_string'
to_var='To_string'

string=<<MESSAGE
To: #{to_var}
From: #{from_var}

Dear #{to_var}
  Please accept attached.
  Your faithfully
    #{from_var}

MESSAGE

puts string
```


 


