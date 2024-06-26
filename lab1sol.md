﻿# Lab 1 & 2 Solution

data: [transplants.dta](https://jhustata.github.io/basic/_downloads/34a8255f06036b44354b3c36c5583d7e/transplants.dta)

Please use this lab as an opportunity to review the course material and prepare yourself for the homework 1 & 2 questions. An answer key will be on Friday April 5, 2024. Question 14 will prepare you for homework 1. The other solutions introduce conditional statements and macros, which are a key part of homework 2.

1. Start Stata and open your do-file editor. [lab1sol.do](https://raw.githubusercontent.com/jhustata/basic/main/lab1solution.do)

2. You will now write your first do-file following the guidelines from [lecture1.do](https://raw.githubusercontent.com/jhustata/basic/main/lecture1.do)
   - Read [about](https://www.stata.com/support/faqs/web/common-connection-error-messages/) `set timeout1 180`
   - Helpful when your internet connection is slow, as was the case at Hopkins in week 1
   - A few of you got error messages when you attempted to import the dataset from its remote location

3. We want to load `transplants.dta`. But before that, let’s check your working directory. See the bottom left side of the console (the main Stata window). You may also type `pwd` on the console. Is it where your `transplants.dta` is located? If not, use one of these two methods:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; a) Next time, launch Stata by double-clicking on `transplants.dta`.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; b) Type `cd c:\your\actual\path` (windows OS) on the console (NOT in your do file). In class and on my Mac OS my directory was `/Users/d/desktop`
    
4. Now let’s get back to your do file. Load `transplants.dta` (double-click on the file or type `use transplants.dta, clear`

5. How many observations does the dataset have? 

```stata
count
di c(N)
di _N
```

6. How many adults (age>18) does the dataset have?

```stata
count if age>18
```

7. How many observations have missing bmi?

```stata
count if missing(bmi)
```

8.  Generate a new variable called agecat. The value of agecat is 1 for patients younger than 18, 2 for those from 18 to 65, and 3 for those older than 65.

```stata

//method 1
generate agecat=.
replace agecat=1 if age<18
replace agecat=2 if age>=18 & age<=65
replace agecat=3 if age>65 & !missing(age)

//method 2
gen byte agecat = 1+(age>=18)+(age>65) if !missing(age)

```

9. What are the means of age and bmi?

```stata
sum age bmi
```

10. Now preserve your dataset (type `help preserve` to learn more).

```stata
preserve
```

11. Drop all patients who are younger than 18 or older than 65, or have missing value for age.

```stata
drop if age<18 | age>65 | missing(age)
```

12. Again, what are the means of age and bmi? restore the dataset. Yet again, what are the means of age and bmi?

```stata
sum age bmi
restore
sum age bmi

```

13. What happened? Leave a comment on your do-file explaining what you just did. Remember, your homework (and all other) .do file scripts should have 1-3 comments per block of code. Do not use your comments/annotation to define the Stata commands you've used. Thats what the `help` command is for. Instead, give yourself or a reader some context.

```stata

// ¯\_(ツ)_/¯

```

14. Lab 1 is almost over. Let Stata say "that was easy!"

```stata
di "that was easy!"
```

15. The last bit. Close your log file. Never forget to close log files! If you hadn't created a log file, this is a reminder to do so. 

```stata
log close 
```

16. You have all your commands so far in your do file, right? Run your entire do file and make sure your do file does exactly the same thing.




