2025-08-30 09:52
Status: #baby
Tags: [[productivity]]
## Main

## Deck Options Explained
### New cards
#### Steps
Khi có cards mới, ta sẽ định nghĩa cách thức học cho bản thân thông qua các steps
Để sang được 1 step mới đối với new/learn card, bạn cần nhấn `Good` mỗi khi xem card
> Your learning steps: 10  30  1440
> - Cái đầu (10) dành cho nút `Again`. Each time you press again on a new/learn card, it’s interval will be 10 minutes, meaning that anki will show you that card in 10 minutes
> - The second number (30) is the first learning step. when you first see a new card, if you press “Good” on it, it’s interval will be 30 minutes, meaning that anki will show you the card again in 30 minutes.
> - The third number (1440 = 1 day) is the second learning step. when you have pressed good on a new card, the second time when you see it, if you press “Good” on it, it’s interval will be 1440 minutes (1 day), meaning that anki will show you that card again in 1 day

Now that you have finished learning steps, the cards exits learning phase and it’ll get an ease (Starting ease) and it will be a graduated card

#### Graduating interval
When you finish learning a card (when you finish learning steps) after you see the card again, it’s interval will be “Graduating interval”
> Say your graduating interval is 3 days and your learning steps are like this =>10 30 1440  
when you see you card after last learning step (after 1 day) if you press “Good” on that card, it’s interval will be 3 days, meaning anki will show you the card again after 3 days.

from there on the interval will be calculated based on your performance and review settings.

####  Easy interval
it controls easy button interval for cards in learning phase
If you press “Easy” on a card in any learning step, the card will graduate (it’ll exit the learning phase) it’s interval will be “Easy interval”
> Say your Easy interval is 4 days.  
if you press easy on a card in learning phase, it’s interval will be 4 days, meaning anki will show you that card again in 4 days

#### Starting ease
Anki will give each card in review phase a unique ease which controls how often you see a card.  
Starting ease is the ease that anki gives cards when they exit learning phase and get graduated.  
You’ll see how it affects how often you see a card in “Reviews”

#### Examples
**Steps (in minutes): 10 30 1440  
Graduating interval: 3 days  
Easy interval: 4 days**

> -  new card -> (Press “Good”) -> show again in 10 minutes  
> - the same card after 10 minutes is passed -> (Press “Good”) -> show again in 30 minutes  
> - the same card after 30 minutes is passed -> (Press “Good”) -> show again in 1 day
> - the same card after 1 day is passed -> (Press “Good”) -> show again in 3 days

-   If you press again in any of those steps, the card will go back to the first learning step
-   if you press hard in any of those steps, the card will stay in that step. it’s interval will be Previous interval (sometimes it’s interval is average of good and again intervals)
-   if you press Easy in any of those steps, the card will exit learning phase, and it’s interval will be 4 days (Easy interval).

#### Difference between graduated cards and cards in learning phase
The difference is in the card’s ease. a card in learning phase doesn’t have ease, and no matter how many times you press “Again” on that card, it won’t affect it’s ease. but for the graduated cards, each time you press again anki will decrease that card’s ease by 20% which will affect all future reviews for that card. (Explanation is review settings)

### Reviews
Scheduling for review cards is based on previous interval (how long it’s been since you last reviews the card to be exact) and **easy bonus**, **interval modifier**, **hard interval**, card’s **ease**.  
each one of these plays a role based on what button you have pressed.
#### Again
if you press **Again** on a review card, it’s exit review state and will enter re-learning phase and it’s ease will be decrease by 20% (more about re-learning phase in **lapses**)
#### Hard
if you press **Hard** on a review card, it’s previous interval will be multiplied by **Hard interval** and it’s ease will be decreased by **15%** telling anki to show you the card more frequently
> _Previous interval: 10 days  
Hard interval: 120%_
review card that you reviewed 10 days ago -> (Press “Hard”) -> show again in 12 days (10\* 1.2) [-15% ease]  
same card after 12 days -> (Press “Hard”) -> show again in 14 days (12 \* 1.2) [-15% ease]  
same card after 14 days -> (Press “Hard”) -> show again in 17 days (14 * 1.2) [-15% ease]
#### Good 
if you press **Good** on a review card, it’s previous interval will be multiplied by card’s **ease**
> _Previous interval: 10 days  
Ease: 200%_
> 
review card that you reviewed 10 days ago -> (Press “Good”) -> show again in 20 days (10 \* 2)  
same card after 20 days -> (Press “Good”) -> show again in 40 days (20 \* 2)  
same card after 40 days -> (Press “Good”) -> show again in 80 days (40 * 2)
#### Easy
if you press **Easy** on a review card, it’s previous interval will be multiplied by **(Ease * Easy bonus)** and it’s ease will be increased by **15%**
>_Previous interval: 10 days  
Ease: 200%  
Easy bonus: 150%_
> review card that you reviewed 10 days ago -> (Press “Easy”) -> show again in 30 days (10\* 2 \* 1.5) [+15% ease]  
same card after 30 days -> (Press “Easy”) -> show again in 97 days (30 \* 2.15  \* 1.5) [+15% ease]  
same card after 97 days -> (Press “Easy”) -> show again in 334 days (97 \* 2.3 \* 1.5) [+15% ease]
#### Interval modifier
all intervals for review cards will be multiplied by interval modifier
There are 2 things that limit how much interval modifier can decrease the interval:
-   Hard interval can’t be less than previous interval
-   Good interval can’t be less than hard interval

so if a buttons interval is less than previous interval, anki will automatically change it to previous interval
Here are the same examples with an interval modifier of 80%:
##### Hard
> _Previous interval: 10 days  
Hard interval: 120%  
Interval Modifier: 80%_

> review card that you reviewed 10 days ago -> (Press “Hard”) -> show again in 10 days (10 \* 1.2 \* 0.8 = 9.6 -> automatically changed to 10) [-15% ease]  
same card after 10 days -> (Press “Hard”) -> show again in 10 days (10\* 1.2 \* 0.8) [-15% ease]  
same card after 10 days -> (Press “Hard”) -> show again in 10 days (10\* 1.2 \* 0.8) [-15% ease]

##### Good 
> _Previous interval: 10 days  
Ease: 200%  
Interval Modifier: 80%_

> review card that you reviewed 10 days ago -> (Press “Good”) -> show again in 16 days (10 * 2 * 0.8)  
same card after 16 days -> (Press “Good”) -> show again in 26 days (16 * 2 * 0.8)  
same card after 26 days -> (Press “Good”) -> show again in 41 days (26 * 2 * 0.8)

##### Easy 
> _Previous interval: 10 days  
Ease: 200%  
Easy bonus: 150%  
Interval Modifier: 80%_

> review card that you reviewed 10 days ago -> (Press “Easy”) -> show again in 24 days (10 * 2 * 1.5 * 0.8) [+15% ease]  
same card after 24 days -> (Press “Easy”) -> show again in 62 days (24 * 2.15 * 1.5 * 0.8) [+15% ease]  
same card after 62 days -> (Press “Easy”) -> show again in 171 days (62 * 2.3 * 1.5 * 0.8) [+15% ease]

### Lapses
Controls scheduling for cards in re-learning phase.
#### Steps 
it’s the same thing as learning steps for new card.  
when you fail a card (press “Again”) the card enters re-learning phase (same as learning phase) and before it becomes a review card again, you’ll have to pass all re-learning steps or press easy on the card.
#### New interval 
it works as the graduating interval in New cards tab. the difference is that you can set it based on cards previous interval.

> _Previous Interval: 50 days  
Steps (in minutes): 10 30 1440  
New interval: 50%_

> review card that you reviewed 50 days ago -> (Press “Again”) -> show again in 10 minutes  
same card after 10 minutes -> (Press “Good”) -> show again in 30 minutes  
same card after 30 minutes -> (Press “Good”) -> show again in 1 day  
same card after 1 day -> (Press “Good”) -> show again in 25 days (50 \* 0.5 | previous interval \* new interval)

if you press “Easy” in any of those steps this is what happens:  
card -> (Press “Easy”) -> show again in 25 days (50 \* 0.5)

#### Minimum interval
it controls the minimum interval for a lapsed card.
> _Previous interval: 10 days  
steps (in minutes): 10 30 1440  
New interval: 20%  
Minimum interval: 5 days_

> review card that you reviewed 10 days ago -> (Press “Again”) -> show again in 10 minutes  
same card after 10 minutes -> (Press “Good”) -> show again in 30 minutes  
same card after 30 minutes -> (Press “Good”) -> show again in 1 day  
same card after 1 day -> (Press “Good”) -> show again in 5 days (10 \* 0.2 = 2 which is less than the minimum interval (5 days) so anki automatically changes it to 5 days)

### Fuzz factor
When you press a button that say 30 days, anki might give the card a different interval. it’s due to fuzz factor and doesn’t mean anki’s algorithm is broken or it’s not functioning properly.  
anki automatically applies a fuzz factor to all cards so when you introduce some new cards, you won’t have to review all of them in the same day.
The fuzz factor is usually between 15 to 20 percent

> _Interval for card A: 10 days (on any button)  
interval for card B: 20 days (on any button)  
interval for card C: 30 days (on any button)  
interval for card D: 40 days (on any button)_

Now here’s the interval that we expect anki to give these cards:
> **for card A the interval should be something from 8 to 12 days  
for card B the interval should be something from 16 to 24 days  
for card C the interval should be something from 25 to 35 days  
for card D the interval should be something from 34 to 46 days**

## References
