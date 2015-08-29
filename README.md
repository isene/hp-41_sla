# hp-41_sla
## HP-41: Calculate guaranteed uptimes for a system composed of serial and paralell components

This program is useful for calculating system uptime guarantees as part of Service Level Agreements (SLAs).

To use the program, XEQ “SLA” and you will see a simple menu “+ SP EP”. This shows the meaning of labels A, B and C:

Here is the key mapping (what shows in the programs menu is in parenthesis):

Label (Menu)	|Description
----------------|-----------
SLA	|Starts the SLA program. Shows the mapping for the top keys so that you don’t have to remember this list.
LBL A (+)	|Add a new component to the system (key inn the percentage guaranteed uptime and press “A”).
LBL B (SP)	|Start input of a parallel system.
LBL C (EP)	|End input of parallel system (adds the redundant component automatically to the overall system as LBL C ends in a GTO A).
LBL D (T)	|Gives the allowed downtime for the system in HH.MMSS format. Input is “guaranteed uptime” in T register, “hours per day” in Z register, “days per week” in Y register and “time period in days” in X register.

Example:

Calculate the guaranteed uptime of the following system.

![alt text](http://dl.dropbox.com/u/73825672/Graphics/sla.png "An example system for SLA")

Here’s how:

```
Instructions                Input       Keys        Output

Start the program                       XEQ "SLA"   "+ SP EP"
Enter system A guarantee    99,999      A           99,9990
Enter system B guarantee    99,8        A           99,7990
Start parallel system                   B            1,0000
Enter system C guarantee    99          A           99,0000
Enter system D guarantee    99          A           99,9900
Enter system E guarantee    99          A           99,9999
End parallel system                     C           99,7989
Enter system F guarantee    99,5        A           99,2999
Find allowed downtime over
30 days for an SLA 8-16
per day, 5 days/week         8          Enter        8,0000
                             5          Enter        5,0000
                            30          D            1,1201
```

The output is the guaranteed uptime so far, except when a parallel system is entered, then the intermediate value for the parallel system is shown.

As you can see, the total guaranteed uptime for the whole system is 99,3%. System F is the singel component wasting the investment in system A and the redundant stack C-E.

The 99,3% uptime guarantee allows for a maximum downtime of 1 hour and 12 minutes during a 30 days period where the SLA coverage is 8 hours, 5 days per week.
