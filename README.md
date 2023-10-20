# dali-lab-courses

I only used the Dartmouth - Courses.csv file

Admittedly, I got really focused on the data imputation and the creating/refining of my model so I kind of didn't follow the theme that much sorry...

**Explanation:**

I tried to explain most of what was going on/what I did in the comments and through the notebook but I'll try to also run through it here (I'll also explain more of the data imputation here since I didn't do it that much in the code).

**Data Imputation**

I encompassed both more algorithmic/logical techniques along with eventually some machine learning data imputation with like a KNN imputer to fill in certain values.  The kind of progression of my data can be seen in the excel file.  The first step in my data imputation involved fixing the Year, Term Number, and some of the Department column.  Just by observing the data, these columns are orderded, so in the case where there was a missing value, my algorithm filled it in with a neighboring value (doesn't really matter) IF both of the neighbors were the same.  Now this worked perfectly for the Year and Term Number columns, but there were still missing values in the Department column due to a multitude of factors such as multiple empty spaces and if the above and below row values were different.

So to fix the Department column, I addressed many of the main edge cases.  For instance, if the nearest non-empty above and below values were not the same, I looked over at the Course Number, which I noticed in each Department was ordered. To briefly explain the logic, if the current course number is greater than the previous one, that means this empty Department value should be in the same Department as the previous row (because they are ordered).  The reverse is also the same.  If that logic didn't work, I also checked if the term number changed over, indicating a change in Department (there were like 1-2 cases where this happened).  But there were even more edge cases that I had to deal with (hence the use of a lot of if statements), such as if the Course Number value in the row was ALSO missing, or if the neighboring Course Number values were also missing. This part honestly took forever to figure out.


**Model Creation**

I'll explain this less
