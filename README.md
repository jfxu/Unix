Unix
====

Helpful Unix Commands

// Find the files in the current directory and subdirectory and then delete them

find . | xargs grep -l "string" | awk '{print "rm "$1}' > doit.sh

gvim doit.sh // check for murphy and his law

source doit.sh

// Specify the file type

find . -name "*.sas" -o -name "*.log" | xargs grep -l "string" | awk '{print "rm "$1}' > doit.sh
