# Quick Guide to Labelling Data for Common Seaborn Plots

![rw-book-cover](https://readwise-assets.s3.amazonaws.com/static/images/article0.00998d930354.png)

## Metadata
- Author: [Kaili Chen](Kaili%20Chen)
- Full Title: Quick Guide to Labelling Data for Common Seaborn Plots
- Category: #articles
- URL: https://medium.com/p/736e10bf14a9

## Highlights
- # label each bar in barplot
  for p in ax.patches:
  # get the height of each bar
  height = p.get_height()
  # adding text to each bar
  ax.text(x = p.get_x()+(p.get_width()/2), # x-coordinate position of data label, padded to be in the middle of the bar
  y = height+100, # y-coordinate position of data label, padded 100 above bar
  s = ‘{:.0f}’.format(height), # data label, formatted to ignore decimals
  ha = ‘center’) # sets horizontal alignment (ha) to center
