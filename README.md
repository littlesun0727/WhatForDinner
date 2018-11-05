# The-cleverest-guy-in-this-planet

##Introduction

In this project, you will provide recommendations for our customers who want to choose a place to eat. Here, our recommendations are based on both his preferences and his location.

To come to our final result, we have overall three processes.

We first generate a function to screen all the restaurants in the New York City based on our customer’s preferences.

Second, using the k-means method in machine learning, we will generate his classification visualization of restaurants based on his location and the Yelp academic dataset/Google map dataset. In this visualization, our customers is segmented into regions, where each region is shaded by the predicted rating of the closest restaurant (yellow is 5 stars, blue is 1 star). Specifically, the visualization you will be constructing is a scatter plot in a diagram.

In the map above, each dot represents a restaurant. The color of the dot is determined by the restaurant's location. For example, downtown restaurants are colored green. The user that generated this map has a strong preference for Southside restaurants, and so the southern regions are colored yellow.

Finally, we come to our finally recommendation based on our customers’ preference and location using the two functions above. We will provide him with a visualization of restaurants, which includes the dot of his location and the dots of locations of our final recommended restaurants.

##Approach

Approach to Getting Our Dataset
As to get data of restaurant in New York, we’ve come up with two ways.

One is to get our dataset from Yelp. Yelp provides data in the form of json objects. Another way is to get our data from Google API. The Google API also returns data in the json object form.

We will use some build-in function of python’s json module to load these data and set up our restaurant dictionary based on these data. We hope to get name, location and other specific the restaurants in New York for further processing.

If both of the two ways don’t work, web-scraping method may also be used for getting our necessary data for further processing. But compared with the web-scraping method, json object is prettified and thus easier for comprehension.

Approach to Processing Our Data
The data of restaurants is clustered by k-means method. K-means clustering aims to partition n observations into k clusters in which each observation belongs to the cluster with the nearest mean, serving as a prototype of the cluster. So the restaurants on map will be segmented into k clusters by k-means method.

By checking which sector the user is in, we can easily tell restaurants in the shortest distance with the user.

Compared with calculating the distances between the user and every single restaurant in the dataset directly, we just need to tell which cluster our user is in. The computational complexity is much less the former direct method, which can be more than 10,000 for each request. In this case, our model can be much more efficient, especially when the amount of users is large.

Approach to Present Our Result
We present our result in a visualized way. The final result that our user get will be a map marked with points which represents restaurants that is selected by the user’s preference in our pre-segmented cluster. An assistive toolbox called mapbox is used.

##Methodology

restaurants.py: Scraping Yelp website, get the dataset of locations, restaurant names and links to restaurant details of all New York City restaurants.
search.py: Given the keyword of filtering and original restaurant dataset, output all matching restaurants.
clusters.py: Given the original restaurant dataset, implement the k-means algorithm, a method for grouping data points into clusters by determining their center positions, to classify it into k clusters.
visualization.py: Given the information of restaurants, draw a scatterplot on the map and add a tag (including restaurant name, business hour, rating and website link) to each scatter point.
what_for_dinner.py (main function for this project): Given the location and requirements of a customer, find restaurants near him meet the requirements. Visualize the outcome on a map.
Discussion

We faced a problem when choosing restaurants near the customer. Firstly, we try to calculus the distance between the customer and every restaurant then set a constraint. If the distance is smaller than the constraint, then we will select it. However, there are thousands of restaurants in New York City and our customer is not only one person. Assume there are LaTeX: N N  customers using this service and LaTeX: M M  restaurants in New York City, the Big-O of this algorithm is:

LaTeX: O\left(MN\right) O ( M N )

As  and  are both quite large, this algorithm is not efficient in solving practical problems.

To optimize this algorithm, we firstly use K-means clustering method to group all the restaurants in to LaTeX: K\:\left(K\ll M\right) K ( K ≪ M )  clusters. Then calculus the distance between the customer and the centroid of each cluster. Finally, we choose the restaurants in the cluster whose outcome is the smallest as the outcome. At this time, the Big-O is:

LaTeX: O\left(KN\right)\:where\:K\ll M O ( K N ) w h e r e K ≪ M

The efficiency of the algorithms improves a lot.
