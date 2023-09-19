----
# Explanation

Obviously, if your training data is full of *errors*, *outliers*, and *noise* (e.g., due to poor-
quality measurements), it will make it harder for the system to detect the underlying
patterns, so your system is less likely to perform well. *It is often well worth the effort
to spend time cleaning up your training data. The truth is, most data scientists spend
a significant part of their time doing just that*. The following are a couple examples of
when you’d want to clean up training data:

- If some instances are *clearly outliers*, it may help to simply discard them or try to
fix the errors manually.
- If some instances are *missing a few features* (e.g., 5% of your customers did not
specify their age), you must decide whether you want to *ignore this attribute*
altogether, *ignore these instances*, *fill in the missing values* (e.g., with the median
age), or train one model with the feature and one model without it.