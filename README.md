# Network Analysis of Reddit Hyperlinks Dataset

## Introduction

Reddit is made up of thousands of communities (subreddits) that connect through shared discussions and links. This report dives into how these subreddits interact, which ones are the most influential and how information flows between them. By using network analysis, we break down key metrics like degree centrality and betweenness to get a clearer picture of how these communities are connected and what that means for online conversations.

## Objective

The objective of this research is to conduct a network analysis on the Reddit Hyperlinks Dataset from the Stanford Large Network Dataset Collection. The goal is to explore relationships within the dataset, determine their connectivity, generate meaningful research questions and apply network analysis techniques to extract meaningful insights using NetworkX, Pandas and Matplotlib.

## Dataset Overview

The two-dataset selected for this analysis are named “soc-redditHyperlinks-body” and “soc-redditHyperlinks-title” the dataset contains records of hyperlinks posted between different subreddits on Reddit. The key columns in the dataset include:

- `source_subreddit`: The subreddit from which the hyperlink originates.  
- `target_subreddit`: The subreddit that receives the hyperlink.  
- `post_id`: A unique identifier for the Reddit post.  
- `timestamp`: The time the hyperlink was posted.  
- `link_sentiment`: The sentiment score of the link.  
- `properties`: Additional link properties.  
- `year`: The year the link was posted.  

## Methodology

### Tools & Libraries Used

The analysis was conducted using Python, with the following key libraries:

- **Pandas**: For data manipulation and preprocessing.  
- **NetworkX**: For building and analyzing the subreddit network graph.  
- **Matplotlib & Seaborn**: For data visualization.  
- **NumPy**: For numerical operations.  

## Research Questions

This analysis seeks to answer the following research questions:

1. Are there subreddits that only receive links but never link to others?  
2. What is the average shortest path length between subreddits in the largest connected component?  
3. Which subreddits receive the highest number of negative sentiment links?  
4. What are the top 10 subreddits with the highest closeness centrality in the subreddit network?  
5. Which subreddits have high degree centrality but low betweenness centrality?  
6. How many unique subreddits exist in the dataset, and which ones are linked the most?  

## Data Preprocessing

### Loading and Inspecting Data

The dataset was loaded using Pandas, and displayed the first few rows:

![image](https://github.com/user-attachments/assets/08ebca84-c47e-44c6-ad46-fbe41d641bd6)

The dataset contains 7 columns, each representing different aspects of the Reddit hyperlink network.

### Handling Missing Values

A check for missing values showed minimal data loss, so standard imputation techniques were carried out to check for missing values and the result shows there are no missing values in the dataset.
![image](https://github.com/user-attachments/assets/6df0aa4d-9ae3-4d69-88f0-7702dad4dd63)

### Data Merging Process

The datasets have been successfully merged, combining information from both the body and title datasets. Below are key observations regarding the merge process:
![image](https://github.com/user-attachments/assets/171d9502-98f3-4c78-a97d-2e96ef50b2d6)

- **Total Records**: The merged dataset contains 858,488 entries with 7 columns.  
- **Column Structure**:  
  - `SOURCE_SUBREDDIT`: The subreddit that posted the link  
  - `TARGET_SUBREDDIT`: The subreddit that received the link  
  - `POST_ID`: Unique identifier for each post  
  - `TIMESTAMP`: The time the post was made  
  - `LINK_SENTIMENT`: Indicates sentiment (positive, neutral, or negative)  
  - `PROPERTIES`: Additional post metadata  
  - `DATASET`: A new column added to distinguish between the two original datasets (body and title)  

## Network Analysis and Visualization Process

### Dataset Sampling for Improved Connectivity

To ensure a more interconnected network, a subset of 1,000 data points was randomly selected from the dataset. This sampling process helps reduce noise while retaining meaningful relationships between subreddits.

![image](https://github.com/user-attachments/assets/82cf31b2-8ed7-4793-bdab-2203f57e9c6a)

### Graph Construction Using NetworkX

An undirected graph was created using the NetworkX library, where each subreddit represents a node, and the edges between them represent interactions based on link sentiment scores. The edges were added by iterating through the sampled dataset, establishing connections between source subreddits and target subreddits with assigned weights.
![image](https://github.com/user-attachments/assets/4855506b-2ad7-4101-ac8f-06edcd91b614)

### Refining the Network Structure

To enhance the network's clarity and relevance, the largest connected component was extracted, ensuring that only the most significant interactions were analyzed. Additionally, a k-core decomposition (k=2) was applied to remove weakly connected nodes, retaining only those with a minimum degree of connectivity. These steps eliminated noise, improved visualization, and highlighted key subreddit relationships.
![image](https://github.com/user-attachments/assets/ddb21134-8c88-4c2a-a49e-55428afccc53)

### Graph Visualization

To make the network easier to interpret, a spring layout was used, which naturally spaces out the nodes based on their connections. Each node was colored blue, while edges were shown in gray to create a clear distinction. The final graph, consisting of 91 nodes and a sampled set of edges, effectively highlights the relationships and interactions between different subreddits.

![image](https://github.com/user-attachments/assets/2703a6c7-1a3c-45b9-b384-dc5dfc9cdd66)

## Analysis of Research Questions

### Are There Subreddits That Only Receive Links but Never Link to Others?

The analysis identified 11,317 isolated subreddits (32.7%) that only receive links but never link out, while 67.3% were connected.
![image](https://github.com/user-attachments/assets/a4fb4439-9b31-4122-be2d-13f6e43f2a5c)

A sample of isolated subreddits includes `violins`, `shopping`, `botcraft`, and `polyamoryr4r`. This suggests that a significant number of subreddits passively receive links without active engagement in link-sharing.

A pie chart visualizes this distribution, with isolated subreddits in red and connected ones in green.
![image](https://github.com/user-attachments/assets/d197ec0b-1ae4-421d-a6db-c80abad5389b)

### What is the Average Shortest Path Length Between Subreddits in the Largest Connected Component?
![image](https://github.com/user-attachments/assets/5933bfab-2142-4b65-956c-b03004540cb7)

The average shortest path length shows how easily subreddits in the largest connected group are linked. In this case, the average path length is **3.80**, meaning it takes about four steps to get from one subreddit to another. This helps us understand how closely connected the subreddits are and how information might flow between them.

### Which Subreddits Receive the Highest Number of Negative Sentiment Links?

Some subreddits receive more negative sentiment links than others. To identify them, we counted the number of negative links directed at each subreddit and highlighted the top 10 most affected ones.
![image](https://github.com/user-attachments/assets/8e3218a7-d572-41cb-a3f7-2c079d25de57)

A bar chart visualizes these subreddits, with the one on the far left receiving the highest number of negative links.
![image](https://github.com/user-attachments/assets/515543f1-1ee1-476f-a4b4-449e6112a1f6)


### What Are the Top 10 Subreddits with the Highest Closeness Centrality?

Closeness centrality measures how easily a subreddit can reach others in the network.
![image](https://github.com/user-attachments/assets/23a6a748-5529-434f-b6f8-f133f5dffc73)

The top 10 subreddits with the highest closeness centrality are the most efficiently connected, meaning they can quickly interact with other communities.
![image](https://github.com/user-attachments/assets/0f3d68c1-fed7-4af8-a581-8bd6c1390e0f)
A bar chart highlights these subreddits, showing which ones act as central hubs for communication and information flow.

### Which Subreddits Have High Degree Centrality but Low Betweenness Centrality?

This analysis identifies subreddits with high degree centrality (many connections) but low betweenness centrality (not key bridges). By selecting the top 1,000 most connected subreddits and computing centrality measures, we filtered those with `degree > 0.01` and `betweenness < 0.001`.
![image](https://github.com/user-attachments/assets/a51f3950-a5ce-4d19-b21e-fe117e494af9)

A scatter plot visualized these relationships.
![image](https://github.com/user-attachments/assets/c329a0ac-b45f-4da5-9135-a871c417f19e)
These subreddits are locally influential but not major connectors in the network, making them ideal for engagement but not for cross-community influence.

### How Many Unique Subreddits Exist in the Dataset, and Which Ones Are Linked the Most?

This analysis explores the number of unique subreddits and identifies the most linked ones.
![image](https://github.com/user-attachments/assets/4ac3397f-2c09-468d-9eb9-d5df692b7bde)
The dataset contains **35,776 unique subreddits**, determined by combining the source and target subreddit lists.

![image](https://github.com/user-attachments/assets/c729f8e7-c7dc-4a66-82ba-04ce245f777f)
A bar chart visualizes the top 20 most linked subreddits, highlighting the most referenced communities. These highly linked subreddits likely serve as major discussion hubs or information sources within the network.

## Key Findings

- **Isolated Subreddits**: Around 32.7% (11,317) of subreddits only receive links but don’t link out to others. This suggests that many communities are being talked about rather than actively engaging in conversations.
- **Average Shortest Path Length**: In the largest connected part of the network, it takes an average of 3.8 steps to get from one subreddit to another, meaning information spreads quickly.
- **Negative Sentiment Links**: Certain subreddits receive more negative sentiment links, which could indicate they are more divisive or criticized by others.
- **Closeness Centrality**: The top 10 subreddits with the highest closeness centrality are the key players, making it easier to reach other parts of the network.
- **Degree vs. Betweenness Centrality**: Some subreddits have a lot of direct connections (high degree centrality) but don’t serve as bridges between different groups (low betweenness centrality). These subreddits are influential in their niche but don’t necessarily connect broader communities.
- **Unique Subreddits & Most Linked Ones**: There are 35,776 unique subreddits, but only a small fraction gets the most attention, dominating the conversation flow.

## Conclusion

This analysis shows that Reddit Hyperlinks Dataset reveals key network patterns, including the presence of isolated subreddits, influential communication hubs, and varying sentiment distributions. The insights from this analysis can help in understanding online communities, their connectivity, and the way information spreads across different subreddits.

## References

- Stanford Large Network Dataset Collection: [https://snap.stanford.edu/data/](https://snap.stanford.edu/data/)  
- NetworkX Documentation  
- Matplotlib & Pandas Official Docs  
