# Last day of month in shell script

## How to get the last day of month in shell script?

### Bash or sh with gnu date

The idea is to use the "minus one day" operation passing to the command the first day of the month after the one you want to know the last day of.

#### Theory:

    I want to know what is the last day of October 2016
    So I ask gnu date to subtract 1 from November 1st, 2016
    It will give me Mon Oct 31

#### Code example:

```shell
$ date -d "2016-11-01 -1 day"
Mon Oct 31 00:00:00
```
More complex example:
#### How to generate a list of first and last days of the months of a given year

Single-line example
```shell
BASED=20141231;for N in `seq 1 12`; do FIRST=$(date -d"$BASED +1 day" +%Y%m%d); MID=$(date -d"$FIRST +1 month" +%Y%m%d);LAST=$(date -d "$MID -1 day" +%Y%m%d); echo "$FIRST - $LAST";BASED="$LAST"; done
```

Multi-line example:
```shell
BASED=20141231
for N in `seq 1 12`; do
  FIRST=$(date -d"$BASED +1 day" +%Y%m%d)
  MID=$(date -d"$FIRST +1 month" +%Y%m%d)
  LAST=$(date -d "$MID -1 day" +%Y%m%d)
  echo "$FIRST - $LAST"
  BASED="$LAST"
done
```

Commented multi-line example:
```shell
# Base date variable, used to get the first day of the next month
# This is the laste day of the previous year
BASED=20141231

# For loop using the result of the seq command, which will give it a list of 1 to 12
for N in `seq 1 12`; do
  # Getting the first day of the month by adding 1 day to the Base date
  FIRST=$(date -d"$BASED +1 day" +%Y%m%d)
  
  # Getting the Middle date, which is a date used to get the last day of the month
  # in fact it is the first day of the next month, obtained by adding 1 month to the
  # first day of the current month in the loop
  MID=$(date -d"$FIRST +1 month" +%Y%m%d)
  
  # Getting the last day of the month by subtracting 1 day from the middle date (see previous step)
  LAST=$(date -d "$MID -1 day" +%Y%m%d)
  
  # Printting out the first and last days of the current month in the loop
  echo "$FIRST - $LAST"
  
  # Setting the new value of BASED to be used in the next loop iteration
  BASED="$LAST"
done
```
