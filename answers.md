# Quiz questions

This is only a "quiz" in the loosest sense that it's asking questions whose
answers will be part of your grade. Please use *any resources you want*, as
long as you list those resources (e.g. peers, websites, etc.)

## Navigating logs

1. What is the SHA for the last commit made by Prof. Xanda on the branch
xanda_0000_movie_processing?
(For this and future questions, the first 5 characters is plenty - neither
Git nor I need the whole SHA.)

9b257

2. What is the SHA for the last commit associated with line 9 of this file?

b2ed3

3. What did line 12 of this file say in commit d1d83?

"2. I should really finish writing this."

4. What changed between commit e474c and 82045?

-    gross_sort = lambda x : x["Gross"]
+    gross_sort = lambda x : int(x["Gross"])

-    top_five = rows[:-5:-1]
+    top_five = rows[:-6:-1]

## Predicting merges

Assume at the start of each of these three questions that your
branch for switching to a top-10 list was called `top_ten`
and your branch generalizing to any number of movies was called `top_N`.
Predict the behavior of these three possible operations - you don't
have to provide a full `diff` but you should describe at a high level
what changes would happen.

These questions are supposed to be separate paths, not cumulative;
for example, you should *not* assume that the operations of 5 were run
before 6. When testing outcomes later in the lab, you should make sure to
revert back to the state of the branch before you started these questions.

5. What do you think would happen if you ran the following commands?
What branches would change, and how?
```
git checkout test
git merge top_N
```

Guess: The first command "git checkout test" ensures that we are on the test branch.
Then, we call "git merge top_N", which merges changes from the "top_N" branch
into the "test" branch. This should result in a merge commit in the "test"
branch that contains the changes from the "top_N" branch. this means that the
"test" branch will change (it includes the "top_N" changes). On the other 
hand, the "top_N" branch will not change.

Actual: Pretty similar to my guess. There were no merge errors!

6. What do you think would happen if you ran the following commands?
What branches would change, and how?
```
git checkout top_ten
git merge test
```

Guess: Here, "git checkout top_ten" ensures that we are on the "top_ten" branch. We 
then do "git merge test", which tries to incorporate changes from the "test" 
branch into the "top_ten" branch. This results in a merge comit in the "top_ten"
branch that contains the changes from the "test" branch.

Basically, the "top_ten" branch will change as it will include the changes 
from the "test" branch. The "test" branch will not change.

Actual: There were merge conflicts. Likely because we changed the quiz.md to 
answers.md in our test, but not in top_ten. There were likely other merge conflicts
as well. <-- Unless I screwed up and there was not supposed to be a merge conflict?

7. What do you think would happen if you ran the following commands?
What branches would change, and how?
```
git checkout test
git rebase top_ten
git rebase top_N
```

Guess: Again, "git checkout test" means that we are now on the "test" branch. We then 
rebase it onto the "top_ten" branch and then rebase it again onto the "top_N"
branch. Basically, this moves the commit history of "test" on top of the commit
history of "top_ten", then "top_N". 

In terms of changes, "test" will be rebased onto both "top_ten" and "top_N",
and "top_ten" and "top_N" branches will not change.

Actual: There was a merge conflict. This occured because when we tried to rebase
the changes from top_N, it conflict with the changes we made earlier in top_ten. 
Basically, whenever it is no longer clear which lines should be maintained, git
complains that it doesn't know what to do, so we must manually alter the code.