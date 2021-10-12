# Data-Visualization
  import numpy as np
  import pandas as pd
  pd.set_option('max_columns', None)
  import matplotlib.pyplot as plt
  import seaborn as sns
  plt.style.use('ggplot')
  import datetime
  from wordcloud import WordCloud
data = pd.read_csv('/content/data.csv')
fig, ax = plt.subplots(figsize=(16,6))
plt.subplot(1, 2, 1)
#kde=kernel density estimate
sns.distplot(data['revenue'], kde=False);
plt.title('Distribution of revenue');

plt.subplot(1, 2, 2)
#calculate the natural logarithmic value of x+1 where x belongs to all the input array elements.
sns.distplot(np.log1p(data['revenue']), kde=False);
plt.title('Distribution of log revenue')
data['log_revenue'] = np.log1p(data['revenue'])
data['log_budget'] = np.log1p(data['budget'])
plt.figure(figsize=(16, 8))
plt.subplot(1, 2, 1)
sns.scatterplot(data['budget'], data['revenue'])
plt.title('Revenue vs budget');
plt.subplot(1, 2, 2)
sns.scatterplot(data['log_budget'], data['log_revenue']) 
plt.title('log transfromation of revenue vs budget');
data.loc[data['homepage'].isnull() == False, 'has_homepage'] = 1
data[['homepage','has_homepage']]
sns.catplot(x='has_homepage', y='revenue', data=data);
plt.title('Revenue for films with and without a homepage');
plt.figure(figsize=(12, 12))
data['log_revenue'] = np.log1p(data['revenue'])
data['log_popularity'] = np.log1p(data['popularity'])
sns.scatterplot(data['log_popularity'],data['log_revenue'])
text =  ' '.join(data['original_title'].values)
wordcloud = WordCloud(max_font_size=None,
                     background_color ='white',
                     width =1200, height =1000).generate(text)
plt.imshow(wordcloud)
plt.title('Top words that are used across movie titles')
plt.axis('off')
plt.show()
plt.figure(figsize=(12, 12))
text =  ' '.join(data['overview'].fillna('').values)
wordcloud = WordCloud(max_font_size=None,
                     background_color ='white',
                     width =1200, height =1000).generate(text)
plt.imshow(wordcloud)
plt.title('Top word across movie overviews')
plt.axis('off')
plt.show()
plt.figure(figsize=(12, 12))
text =  ' '.join(data['all_genres'].fillna('').values)
wordcloud = WordCloud(max_font_size=None,
                     background_color ='white',
                     width =1200, height =1000).generate(text)
plt.imshow(wordcloud)
plt.title('Top genres used in the movies')
plt.axis('off')
plt.show()
