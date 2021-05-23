---
layout: post
title:  "Setting default value for a BASH variable
date:   2020-02-25 10:24:11 +0300
categories: jekyll posts
---

# Setting default value for a BASH variable #
```
    Dec. 8th, 2007 at 9:08 PM
```
To set a default value for a BASH variable, the syntax is: (good for setting default value for a BASH command line parameter)
```
VARIABLE=${1:-DEFAULTVALUE}    #set VARIABLE with the value of 1st Arg to the script,
                                                          #If 1st arg is not entered, set it to DEFAULTVALUE
```
The following simple script illustrate this:
```
tmpdir=/tmp
defvalue=1

DIR=${1:-$tmpdir}   # Defaults to /tmp dir.
VALUE=${2:-$defvalue}           # Default value is 1.

echo $DIR
echo $VALUE
```

Now while running the script, specify values for both the arguments.
```
$ ./defvaue.sh /dev 23
/dev
23
```
This time don't mention their values.
```
$ ./defvaue.sh
/tmp
1
```
so
```
DIR=${1:-$tmpdir}
VALUE=${2:-$defvalue}
```
is a replacement for the following:
```
[ -z $1 ] && DIR="/tmp"
[ -z $2 ] && VALUE=1
```