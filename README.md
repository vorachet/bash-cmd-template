
# Bash shell script template for command-line interfaces.

# Features

 * **bash-cli-template** provides a framework for creating BASH shell command-line interface.
 * **bash-cli-template** provides built-in debug and help command
 * **bash-cli-template** provides built-in validation for mandatory options 
 * **bash-cli-template** provides built-in function to show optional parameters on each command 

# Concept 

**bash-cli-template** comes with **base.sh** and the following framework for creating CLI.

```
# Step 1/5. There are 7 variables you have to define in order to implement the functionality of your script.
# See "Learning by examples" section for details.
#     SCRIPT_NAME
#     DOMAIN_OPTION_NAME[]
#     DOMAIN_OPTION_ALTERNATIVE_NAME[]
#     DOMAIN_OPTION_DATA_TYPE[]
#     DOMAIN_CMD_MANDATORY_OPTIONS[]
#     DOMAIN_CMD_OPTIONS[]
#     DOMAIN_OPTION_INPUT_DESC[]

# Step 2/5. Create a set of shell functions corresponding to the value you defined in DOMAIN_OPTION_NAME[]
#     - You have to understand the concept of DOMAIN_OPTION_DATA_TYPE[]   

# Step 3/5. Define mandatory parameters on each command.

# Step 4/5. Define optional parameters on each command.

# Step 5/5. Add "source ./base.sh" at the end of your script
source ./base.sh

# DONE!
```
# Learning by examples

## helloworld CLI script  

The code example of the helloworld CLI script is available in examples folder. 

You can run the helloworld CLI script with the following steps.

```
$ git clone https://github.com/vorachet/bash-cli-template.git
$ cd bash-cli-template/examples
$ ./helloworld.sh
```

File: helloworld.sh
```
#!/bin/bash

# Implementation of your script 
#     SCRIPT_NAME
#     DOMAIN_OPTION_NAME[]
#     DOMAIN_OPTION_ALTERNATIVE_NAME[]
#     DOMAIN_OPTION_DATA_TYPE[]
#     DOMAIN_CMD_MANDATORY_OPTIONS[]
#     DOMAIN_CMD_OPTIONS[]
#     DOMAIN_OPTION_INPUT_DESC[]

# Script name
SCRIPT_NAME="example1"

# Option name
DOMAIN_OPTION_NAME[0]="-t"
DOMAIN_OPTION_NAME[1]="-u"
DOMAIN_OPTION_NAME[2]="-l"
DOMAIN_OPTION_NAME[3]="hello"

# Alternative option name
DOMAIN_OPTION_ALTERNATIVE_NAME[0]="--text"
DOMAIN_OPTION_ALTERNATIVE_NAME[1]="--uppercase"
DOMAIN_OPTION_ALTERNATIVE_NAME[2]="--lowercase"
DOMAIN_OPTION_ALTERNATIVE_NAME[3]="helloworld" 

# Option data type. It consists of string, boolean, and cmd.
# 	string does not allow you set empty option value
# 	object allows you flag the option without giving value
# 	cmd is the command used in various situations in your script. 
#	cmd may require one or more mandatory or optional parameters
DOMAIN_OPTION_DATA_TYPE[0]='string'
DOMAIN_OPTION_DATA_TYPE[1]='boolean'
DOMAIN_OPTION_DATA_TYPE[2]='boolean'
DOMAIN_OPTION_DATA_TYPE[3]='cmd'

# Setting mandatory parameters for cmd
DOMAIN_CMD_MANDATORY_OPTIONS[3]="0"

# Setting optional parameters for cmd
DOMAIN_CMD_OPTIONS[3]="1,2"

# Option input description
DOMAIN_OPTION_INPUT_DESC[0]="text"
DOMAIN_OPTION_INPUT_DESC[1]="use uppercase"
DOMAIN_OPTION_INPUT_DESC[2]="use lowercase"
DOMAIN_OPTION_INPUT_DESC[3]="To print text from the value of -t"

# Implementation of "hello" command
# 
# DOMAIN_OPTION_VALUE[] is an array managed by the template base.sh
# The number of array items of DOMAIN_OPTION_VALUE[] will be identical to DOMAIN_OPTION_NAME[].
# Possible values on each data type: 
# 
#   Possible values of string data type  =  { "<undefined>" , ... }
#   Possible values of boolean data type =  { 0 , 1 }
#   Possible values of cmd data type     =  { "wait" , "invoked" }
# 
hello() {
    # -t | --text
    TEXT=${DOMAIN_OPTION_VALUE[0]}
    # -u | --uppercase
    ENABLED_UPPERCASE=${DOMAIN_OPTION_VALUE[1]}
    if [ ${ENABLED_UPPERCASE} == true ]; then
        echo ${TEXT} | tr '[:lower:]' '[:upper:]'
        exit
    fi 
    # -l | --lowercase
    ENABLED_LOWERCASE=${DOMAIN_OPTION_VALUE[2]}
    if [ ${ENABLED_LOWERCASE} == true ]; then
        echo ${TEXT} | tr '[:upper:]' '[:lower:]'
        exit
    fi 

    echo ${TEXT}
    exit
}

source ../base.sh

``` 

## Reviewing helloworld CLI script  

# License 

The MIT License (MIT)

Copyright (c) 2015 Vorachet Jaroensawas 

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
