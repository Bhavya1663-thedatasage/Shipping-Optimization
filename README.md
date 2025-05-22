# Shipping-Optimization

=============================
Shipping Optimization Project
=============================

Objective:
Optimize delivery routes from Harrisburg, PA to 19 other U.S. cities using real driving distances, clustering, and route analysis.

Requirements:
- Python 3.8+
- MongoDB instance (local or cloud)
- Google Maps API Key
- Jupyter Notebook or Google Colab
- Install Apache Spark version 3.4.1 or compatible
- Install Java JDK 8 or JDK 11 (if running locally)

Install Dependencies:
Run the following in your notebook or terminal:
  !pip install pymongo
  !pip install googlemaps

(Optional for Spark):
  import findspark
  findspark.init()
  from pyspark.sql import SparkSession

Project Steps:

1. City List Initialization
   - Define a list of 20 cities.
   - Save them into MongoDB under the 'locations' collection.

2. Distance Matrix Generation
   - Fetch all pairwise driving distances using Google Maps Distance Matrix API.
   - Save them as a nested dictionary in the 'distances' collection.

3. MDS Projection
   - Convert the distance matrix to 2D coordinates using 'Multi-Dimensional Scaling (MDS)' from 'sklearn.manifold'.

4. Clustering (KMeans)
   - Apply 'KMeans' to group cities into 4 clusters.
   - Store each city's cluster ID and coordinates in the 'clusters' collection.

5. Representative Cities
   - For each cluster, find the city closest to the cluster centroid.
   - Store these in 'representative_cities' collection.

6. Cluster Ranking
   - Rank clusters by distance from Harrisburg's location.
   - Store the ranked clusters in 'cluster_order'.

7. Route Generation
   - For each cluster, generate all permutations of city orders.
   - For each permutation, compute total route distance using Google Maps API.

8. Data Storage
   - Save the computed routes and their distances to MongoDB under 'cluster_<rank>_routes'.

MongoDB Collections:
- 'locations' - List of all cities
- 'distances' - Distance matrix between cities
- 'clusters' - Cluster IDs and MDS coordinates
- 'representative_cities - Centroids and key cities
- 'cluster_order' - Ranked delivery clusters
- 'cluster_<rank>_routes' - Route permutations and distances

Notes:
- Replace the Google API key placeholder with your actual API key.
- API rate limits may apply — include 'time.sleep()' as needed.
- Ensure the respective environment variables are set up


