Zomato Dataset Analysis & Validation with Pandas

Overview

I dived into a messy Zomato restaurant dataset. The raw data was all over the place—some columns had weird formats, plenty of blanks, and a bunch of values just didn’t make sense. I wanted to figure out which parts of the data made sense, what I could actually use, and what I’d need to treat with extra caution before I even thought about serious analysis.

Problems I Found

Mixed data types

- The ‘rate’ column didn’t just have numbers like ‘4.2/5’—it also had random stuff like ‘NEW’ or just dashes.
- ‘approx_cost’ had commas in the numbers (‘1,200’) and got stored as strings, which made any calculations tricky.

Missing values

- There were blanks in ‘rate’, ‘votes’, ‘cost’, ‘online_order’, and ‘book_table’.
- I didn’t jump to conclusions about why things were missing. First, I looked for patterns.

Invalid values

- I saw negative votes like ‘-5’ and negative costs like ‘-300’. That’s not possible for a restaurant.
- Things like ‘rate’ being ‘NEW’ or ‘-’ don’t mean anything for analysis.
- These weren’t just missing—they were flat-out wrong and needed special attention.

Inconsistent categories

- Sometimes choices like ‘online_order’ were written as ‘Yes’, ‘YES’, or ‘no’. Same thing with restaurant types—‘Cafes’, ‘cafes’, ‘Other’, ‘other’.
- This made grouping and sorting unpredictable.

Duplicate records

- I found the same restaurant popping up multiple times.
- There weren’t timestamps or location data, so I couldn’t always tell if it was a repeat entry or just a mistake. I flagged these as suspicious and kept an eye on them.

Validation Checks I Did

Logical checks

- If a restaurant had a sky-high rating but almost no votes, I labeled it as suspicious.
- When votes or cost were negative, I cut them out from any calculations.

Outlier detection

- I used the IQR method to spot values that were way off from the rest.
- I made sure to separate:
  - values that were outright invalid (shouldn’t be there at all)
  - outliers (rare but possible)
  - suspicious stuff (maybe valid, but questionable)

How I Handled Issues During Analysis

- I excluded all the invalid values from calculations—so things like average rating or total votes wouldn’t get skewed.
- For the suspicious restaurants with high ratings but barely any votes, I kept them around but marked them, just in case.
- I temporarily standardized categories like ‘yes’ and ‘YES’ so I could actually group them.
- I reviewed duplicates but held off on deleting any unless I was totally sure they were the same.

What I Learned

- Just seeing a row pop up multiple times doesn’t make it a true duplicate—you need more context.
- If something looks right (valid format), it doesn’t mean it’s trustworthy. A 4.5 rating with 2 votes isn’t the same as 4.5 with 2,000 votes.
- There’s a world of difference between invalid values, outliers, and stuff that just looks off. Mixing them up steers your results in the wrong direction.
- Analysis isn’t just about running code. You have to make calls and be ready to explain why you handled the data the way you did.

Tools Used

- Python
- Panday

Possible Future Improvements

- Add a confidence score for each rating, based on how many people voted.
- Add something like ‘is_new_restaurant’ to flag newer places separate from the established ones.
- Prep a much cleaner version of the dataset if I ever want to do deeper dives later.

This is exactly how I approached the data. My main focus was figuring out which numbers I could trust and where I needed to watch my step.