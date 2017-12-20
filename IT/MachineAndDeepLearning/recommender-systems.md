#Week 1: Intro
- Informataion retrieval - you have corpus of texts with TFIDF and immediate query
- Content filtering - you have user profile and stream of content
- Collaborative filtering 
user-user is simple but slow because they calculate results "by spot"
Dimensionality reduction and singular value decomposition.
http://spectrum.ieee.org/computing/software/deconstructing-recommender-systems

Analytical framework:
 - Content to recommend. What to recommend?
 - Purpose. For what?
 - Context. what is user doing?
 - whose opinons 
 	- experts
 	- random folks
 	- people like you
 - personalization level
 	- generic\ not-personalized
 	- demographic
 	- ephemeral (match current activity)
 	- persistent (match long-term interests)
 - privacy and trustworthiness
 	- what system knows about me?
 	- biases built-in by provider
 	- transparency, reputation
 - interfaces
 - algorithms
 	- non-personalized summary statistics
 	- content-based filtering
 		- information filtering
 		- knowledge based
 	- collaborative filtering
 		- user-user
 		- item-item
 		- dimensionality reduction (SVD matrixes)
 	- others
 		- critique / intervies bases recommendations
 		- hybrid

Basic model
- users
- items
- ratings 	  	 	