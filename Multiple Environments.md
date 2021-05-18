## Existing at Vulcan
Currently, (actually from 2018-2021), Vulcan IT development team uses three layer multiple environment for CI/CD (continuous integration/ continuous delivery).

> dev -> staging -> production

It works great as we are deploying every feature when it is ready. Also suit for SCRUM organization where push a set of features at the end of the sprint.


## Challenge we meet
We use staging as our testing environment. The feature, main and release branch all could deploy into staging environment. Due to devlopment team's growing, there are six developers. Sometimes, two or more features of the same project are developing.

> E.g.

## Reference
- [**Multiple environments to improve your developer experience** (May 15, 2020)](https://thomaspoignant.medium.com/multiple-environments-to-improve-your-developer-experience-727f72dc39da)
- [**The path to production: how and where to segregate test environments** (Feb 24. 2021)](https://circleci.com/blog/path-to-production-how-and-where-to-segregate-test-environments/)