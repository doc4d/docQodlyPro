---
id: lang-time
title: Time
---

A Time attribute, variable or expression can be in the range of 00:00:00 to 596,000:00:00.

:::info

In [Qodly models](../../cloudOnlyFeatures/model/attributes.md), time attributes have the type **Duration**.

:::

Times are in 24-hour format.

A time value can be treated as a number. The number returned from a time is the number of seconds since midnight (00:00:00) that time represents.


## Time literals  

A time literal constant is enclosed by question marks (?...?).

A time literal constant is ordered hour:minute:second, with a colon (:) setting off each part. Times are specified in 24-hour format.

Here are some examples of time literals:

```qs
?00:00:00? ` midnight
?09:30:00? ` 9:30 am
?13:01:59? ` 1 pm, 1 minute, and 59 seconds
```

A null time is specified by ?00:00:00?

   
## Time operators 

|Operation	|Syntax	|Returns	|Expression	|Value|
|---|---|---|---|---|
|Addition	|Time + Time	|Time	|?02:03:04? + ?01:02:03?	|?03:05:07?|
|Subtraction	|Time – Time	|Time	|?02:03:04? – ?01:02:03?	|?01:01:01?|
|Addition	|Time + Number	|Number	|?02:03:04? + 65	|7449|
|Subtraction	|Time – Number	|Number	|?02:03:04? – 65	|7319|
|Multiplication	|Time * Number	|Number	|?02:03:04? * 2	|14768|
|Division	|Time / Number	|Number	|?02:03:04? / 2	|3692|
|Longint division	|Time \ Number	|Number	|?02:03:04? \ 2	|3692|
|Modulo	|Time % Time	|Time	|?20:10:00? % ?04:20:00?	|?02:50:00?|
|Modulo	|Time % Number	|Number	|?02:03:04? % 2	|0|
|Equality	|Time  ==  Time	|Boolean	|?01:02:03?  ==  ?01:02:03?	|True|
			||||?01:02:03?  ==  ?01:02:04?	|False|
|Inequality	|Time  !=  Time	|Boolean	|?01:02:03?  !=  ?01:02:04?	|True|
			||||?01:02:03?  !=  ?01:02:03?	|False|
|Greater than	|Time >; Time	|Boolean	|?01:02:04? > ?01:02:03?	|True|
	||||		?01:02:03? > ?01:02:03?	|False|
|Less than	|Time &lt; Time	|Boolean	|?01:02:03? < ?01:02:04?	|True|
		||||	?01:02:03? < ?01:02:03?	|False|
|Greater than or equal to	|Time >;=  Time	|Boolean	|?01:02:03? >;= ?01:02:03?	|True|
			||||?01:02:03? >;= ?01:02:04?	|False|
|Less than or equal to	|Time &lt;= Time	|Boolean	|?01:02:03? &lt;= ?01:02:03?|	True|
			||||?01:02:04? &lt;= ?01:02:03?	|False|

### Example 1 

To obtain a time expression from an expression that combines a time expression with a number, use the commands `Time` and `Time string`.

You can combine expressions of the time and number types using the `time` or `currentTime` commands:

```qs
	//The following line assigns to vlSeconds the number of seconds   
	//that will be elapsed between midnight and one hour from now
var vlSeconds, vhSoon : time
vlSeconds = currentTime+3600
	//The following line assigns to $vHSoon the time it will be in one hour
vhSoon = time(currentTime+3600)
```

The second line could be written in a simpler way:

```qs
  // The following line assigns to vHSoon the time it will be in one hour
 vhSoon = currentTime+?01:00:00?
```

### Example 2

The Modulo operator (`%`) can be used, more specifically, to add times that take the 24-hour format into account:

```qs
t1 = ?23:00:00? // It is 23:00 hours
  // We want to add 2 and a half hours
t2 = t1+?02:30:00? // With a simple addition, t2 is ?25:30:00?
t2 = (t1+?02:30:00?)%?24:00:00? // t2 is ?01:30:00? and it is 1:30 hour the next morning
```

