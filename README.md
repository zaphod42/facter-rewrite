Facter
======

This is a redesign and rewrite of facter that pushs all facts to be external
programs which are executed to fetch the data. The programs can either supply a
set of facts outright or they can provide a declaration of what they will
provide when given the value of another fact.
