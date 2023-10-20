# dali-lab-courses

I only used the Dartmouth - Courses.csv file

Admittedly, I got really focused on the data imputation and the creating/refining of my model so I kind of didn't follow the theme that much sorry...

**Explanation:**

I tried to explain most of what was going on/what I did in the comments and through the notebook but I'll try to also run through it here (I'll also explain more of the data imputation thought process here since I didn't do it in the code).

**Data Imputation**

_Year, Term Number, (some) Department_

I encompassed both more algorithmic/logical techniques along with eventually some machine learning data imputation with like a KNN imputer to fill in certain values.  The kind of progression of my data can be seen in the Excel file.  The first step in my data imputation involved fixing the Year, Term Number, and some of the Department columns.  Just by observing the data, these columns are ordered, so in the case where there was a missing value, my algorithm filled it in with a neighboring value (doesn't really matter) IF both of the neighbors were the same.  Now this worked perfectly for the Year and Term Number columns, but there were still missing values in the Department column due to a multitude of factors such as multiple empty spaces and if the above and below row values were different.

_Department_

So to fix the Department column, I addressed many of the main edge cases.  For instance, if the nearest non-empty above and below values were not the same, I looked over at the Course Number, which I noticed in each Department was ordered. To briefly explain the logic, if the current course number is greater than the previous one, that means this empty Department value should be in the same Department as the previous row (because they are ordered).  The reverse is also the same.  If that logic didn't work, I also checked if the term number changed over, indicating a change in Department (there were like 1-2 cases where this happened).  But there were even more edge cases that I had to deal with (hence the use of a lot of if statements), such as if the Course Number value in the row was ALSO missing, or if those neighboring Course Number values were also missing (to solve those, I instead looked for the nearest non-empty course number above and the nearest non-empty course number below and compared). This part honestly took forever to figure out.

_Number of Sections, Enrollments, and Average Section Size_

Next, the Number of Sections, Enrollments, and Average Section Size weren't too difficult, as I just used the logic of Average Sections Size * Number of Sections = Enrollments.  In this trio, if two of the values were present, the third could be easily calculated.  However, this still left a few empty values (because there would sometimes be 2+ empty sections) which I dealt with later.

_Course Number_

Moving onto the Course Number column, this one was also a bit tricky.  As I mentioned earlier, within departments, Course Numbers also appear to be ordered.  The problem is I can't just choose any random number like 12.2342342 because that almost certainly isn't a class.  So I kind of created a "vocabulary" to choose classes from.  Back to the df dataframe, since the Course Number values have to be ordered my algorithm chooses a value in this vocabulary that is in between the current and next Course Numbers.  There were a few edge cases I had to deal with like there is the possibility that this is the last value in the department, so in that case, it just picks a bigger number in the vocabulary.

_KNN Imputer_

FINALLY, to fill in the medians, I used a KNN imputer that imputes the Median GPA using other variables on a separate dataframe, and then it fills the main dataframe's (df) missing values.  I thought a KNN imputer would be better than something like an Iterative imputer because I didn't want it to necessarily look at the entire column.  Choosing the closest neighbors, in my mind, would likely yield more logical imputed data.  Similarly, I did the same to fill in the still empty Number of Sections, Enrollments, and Average Section Size values.  I did the columns one at a time to still maintain the mathematical logic.


**Model Creation**

I'll try to be less wordy here because I do a lot more explaining on some of the hyperparameters and certain decisions I made within the colab notebook.  I used kind of a similar model to my other Seasons! projec but I added a few more things to try to improve it.  Mainly, I added regularization in my hidden layers (l1 and l2) to prevent overfitting and underfitting of my model.  I also employed grid search to tune my hyperparameters, although I know there are better methods.  I validated my data with a model that simply predicted the median of all the Median GPA's everytime and my model didn't do any better.  In hindsight, trying to predict Median GPA wasn't a great idea but oh well.

I think this whole application, learning, coding, and writing explanations for the DALI app took ~20 hours over two-ish weeks.  Sorry if this is long!  Also, I will note that I often used online resources like youtube, websites, github, and sometimes chatGPT to help and learn.
