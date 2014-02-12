Unix
====

Helpful Unix Commands

find . | xargs grep -l "string" | awk '{print "rm "$1}' > doit.sh

gvim doit.sh // check for murphy and his law

source doit.sh
