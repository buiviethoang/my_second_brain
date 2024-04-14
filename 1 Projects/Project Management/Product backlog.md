## Overview
The product backlog is a prioritized list of desired product functionality. It provides a centralized and shared understanding of what to build and the order in which to build it

As long as there is a product or system being built, enhanced, or supported, there is a product backlog.

## Product Backlog Items
The product backlog is composed of backlog items, which I refer to as PBIs, backlog items, or simply items
Most PBIs are **features**, items of functionality that will have tangible value to the user or customer
These are often written as **user stories**

![[Screenshot 2023-10-06 at 09.01.57.png]]

![[Screenshot 2023-10-06 at 09.02.28.png]]

## Good product backlog characteristics
***DEEP***
### Detailed Appropriately
Not all items in a product backlog will be at the same level of detail at the same time
PBIs that we plan to work on soon should be near the top of the backlog, small in size, and very detailed so that they can be worked on in a near-term sprint. PBIs that we won’t work on for some time should be toward the bottom of the backlog, larger in size, and less detailed.
Nếu mà b break down các cái PBI lớn (epic chẳng hạn) mà break down sớm quá, khi chưa đủ dữ kiện -> lâu, b tốn thời gian để get to detail. Muộn quá thì nó khiến cho các kế hoạch bị chậm lại -> just-in-time fashion

![[Screenshot 2023-10-06 at 09.24.09.png]]

### Emergent 
As long as there is a product being developed or maintained, the product backlog is never complete or frozen
The structure of the product backlog is  constantly emerging over time. As new items are added or existing items are refined, the product owner must rebal- ance and reprioritize the product backlog, taking the new information into account.
### Estimated
Each product backlog item has a size estimate corresponding to the effort required to develop the item
![[Screenshot 2023-10-06 at 09.49.31.png]]

The product owner uses these estimates as one of several inputs to help determine a PBI’s priority (and therefore position) in the product backlog
Những thằng to -> cần phải refine, những thằng bé xử lý trc. Size tính theo ngày làm việc hoặc story points.
Không cần estimate quá chính xác, chỉ cần chấp nhận đc. 
### Prioritized 
it is unlikely that all of the items in the backlog will be prioritized
![[Screenshot 2023-10-06 at 09.51.40.png]]



## Grooming
### What is ? 

Grooming refers to a set of three principal activities: creating and refining (adding details to) PBIs, estimating PBIs, and prioritizing PBIs.

![[Screenshot 2023-10-06 at 09.53.35.png]]

### Who Does the Grooming?
Grooming the product backlog is an ongoing collaborative effort led by the product owner and including significant participation from internal and external stakehold- ers as well as the ScrumMaster and development team## Definition of Ready 
![[Screenshot 2023-10-06 at 09.58.52.png]]


Thường thì thằng product owners là thằng quyết định, tuy nhiên thì nên để cho cả team cùng nhâu vào mà estimate -> nó sẽ có đc cái gọi là collectie intelligence và team sẽ có đc nhiều in4 hơn, đôi khi còn gợi mở đc rất nhiều issues mình chưa nghĩ đến. 
Đồng thời cho cả team hiểu rõ hơn hướng đi, và cũng giúp team tech vs non tech hiểu và làm việc tốt vs nhau hơn. 

**Rules**: 10% của sprint time của từng dev nên để support cho việc grooming vấn đề cùng với PO. 
### When Does Grooming Take Place?
Initial grooming occurs as part of the release-planning activity (see Chapter 18 for details). During product development, the product owner meets with the stake- holders at whatever frequency makes sense to perform ongoing grooming.
![[Screenshot 2023-10-06 at 10.05.24.png]]


When working with the development team, the product owner might sched- ule either a weekly or a once-a-sprint grooming workshop during sprint execution.

Sometimes teams prefer to spread out the grooming across the sprint, rather than block out a predetermined period of time
They take a bit of time after their daily scrums to do some incremental grooming
Cái này ko require nhiều người, một số người có kinh nghiệm và liên quan sẽ support PO

Một số team thì thấy trong giai đoạn sprint review. 

## Definition of Ready
Grooming the product backlog should ensure that items at the top of the backlog are ready to be moved into a sprint so that the development team can confidently com- mit and complete them by the end of a sprint.
![[Screenshot 2023-10-06 at 10.11.45.png]]

Some Scrum teams formalize this idea by establishing a definition of ready. You can think of the definition of ready and the definition of done (see Chapter 4) as two states of product backlog items during a sprint cycle. 
*Checklist definition of ready*
1. Business value is clearly articulated.
2. Details are sufficiently understood by the development team so it can make an informed decision as to whether it can complete the PBI.
3. Dependencies are identified and no external dependencies would block the PBI from being completed.
4. Team is staffed appropriately to complete the PBI.
5. The PBI is estimated and small enough to comfortably be completed in one sprint.
6. Acceptance criteria are clear and testable.
7. Performance criteria, if any, are defined and testable.
8. Scrum team understands how to demonstrate the PBI at the sprint review.

## Flow Management 
### Release flow management

The product backlog must be groomed in a way that supports ongoing release plan- ning


![[Screenshot 2023-10-06 at 10.40.20.png]]

- The must-have features represent the items that we simply must have in the upcoming release or else we don’t have a viable customer release.
- The nice-to- have features represent items we are targeting for the next release and would like to include. If, however, we run short of time or other resources, we could drop nice-to- have features and still be able to ship a viable product
- The won’t-have features are items that we’re declaring won’t be included in the current release
### Sprint Flow Management
![[Screenshot 2023-10-06 at 10.45.31.png]]

When grooming for good sprint flow, it is helpful to view the product backlog as a pipeline of requirements that are flowing into sprints to be designed, built, and tested by the team
If the flow of groomed, detailed, ready-to-implement items is too slow, eventually the pipeline will run dry and the team won’t be able to plan and execute the next sprint
On the other hand, putting too many items into the pipeline for refinement creates a large inventory of detailed requirements that we may have to rework or throw away once we learn more (a major source of waste)
=> Nên có vừa đủ product backlog item trong cái inventory thôi => luồng vào và ra sẽ ổn, ko bị ít quá và ko bị lãng phí
Nên có khoảng 2-3 lượng stories tương ứng vs từ sprint sẵn sàng
for example, if the team can normally do about 5 PBIs per sprint, the team grooms its backlog to always have about 10 to 15 PBIs ready to go at any point in time.
## Which and how many product backlogs?
one product, one product backlog, meaning that each product should have its own single product backlog that allows for a product-wide description and prioritization of the work to be done.
### What Is a Product?
![[Screenshot 2023-10-06 at 10.52.55.png]]

if you could put a PID on it, salespeople could include it on an order form and therefore it was a “product.”

A product is something of value that a customer would be willing to pay for and something we’re willing to package up and sell.
### Large Products—Hierarchical Backlogs
On a large product development effort to create something like a cell phone, we can have many tens or hundreds of teams whose work must all come together to create a marketable device. Trying to put the PBIs from all of these teams into one manageable product backlog isn’t practical

To begin with, not all of these teams work in related areas. For example, we might have seven teams that work on the audiovisual player for the phone, and another eight teams that work on the web browser for the phone. Each of these areas delivers identifiable value to the customer, and the work in each area can be organized and prioritized at a detail level somewhat independent of the other areas.
Based on these characteristics, most organizations address the large-product problem by creating **hierarchical backlogs**

![[Screenshot 2023-10-06 at 10.58.47.png]]

1 backlogs tổng, phụ trách mô tả các large-scale features. Có 1 ông **chief product owner** 
Sau đó cũng có nhiều các cái backlogs con cho từng teams phát triển từng feature

### Multiple Teams—One Product Backlog
The one-product-one-product-backlog rule is designed to allow all of the teams working on the product to share a product backlog. Aligning all of the teams to a single backlog enables us to optimize our economics at the full-product level

we put all of the features into one backlog and make them com- pete for priority against all other features, ensuring that the highest-priority features from the full-product perspective are identified and prioritized to be worked on first.

If all of our teams are interchangeable, so that any team can work on any PBI in the one shared backlog, we actually get to realize the prioritization benefit enabled by the single product backlog

To work within this reality, we must know which items in the product backlog each team can work on. Conceptually, we need team-specific backlogs. Conceptually, we need team-specific backlogs. In practice, however, we don’t actually create product backlogs at the team level. Instead, we have team-specific views of the shared backlog
![[Screenshot 2023-10-06 at 11.30.05.png]]
### One Team—Multiple Products
The first, and often the best, solution is to have the team work on one prod- uct at a time. In each sprint the team works only on the items from one product backlog.

if organizational impediments force us to have the single team work on multiple products concurrently, we might consider merging the PBIs for all three products into one product backlog. This would require that the product owners for the three products come together and reach a single prioritization across all of the products.

Even if we choose to maintain three separate product backlogs, every sprint someone (presumably the product owner for the team) will need to assemble a prioritized set of PBIs from the three backlogs and present those to the team for its consideration and commitment.
![[Screenshot 2023-10-06 at 11.36.08.png]]
## Closing
