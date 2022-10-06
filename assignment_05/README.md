# Part 2
corr=sales.corr()
Correlation shows relation bewtween each and every column entities. 
Dark blue color gives the relation between the same column. Dark red gives the relation between column having negative relation.
1.00 gives the correlation for the same column and between 0 and 1 gives the correlation value of columns having positive correlation like between Profit and Revenue.
We can do column wrangling in speed compared to doing it in excel sheet. 
# Part 3
Using numpy we can purform almost every operation which we do in list.<br>
Other intresting operation in numpy we can pass index as a list to print only some specific numbers which we pass in the list.<br>
>b[[0,2,-1]]<br>
> [0,2,-1] is index which will return b[0] , b[2], b[-1]<br>

For multidimensional array we pass rows and column number in a single list<br>
>a[1,0] *This is similar to **a[1][0]** that is second row of first column*<br>

Another example
>a[:, :2] *This means for every row select only first and second column*<br>

We can assign row **or** change row in two ways
>a[1]=np.array[1,3,4]<br>
a[2]=4<br>
*This will change row number two to 1,3,4 and row number three to 4 for what dimension the array have.*

We can perform almost every statsics operation in single and multidimenional array
>a.sum(), a.mean(), a.std()

Also for multidimensional array we can do operation along with axis
>a.sum(axis=0),a.sum(axis=1) *Same for mean and std*

Boolean arrays
>a[a>=2] *a>=2 will return boolean list thus it will return whichever element satifies the condition.

We can perform same for multidimensional array but it will return one dimensional array.<br>
# Part 4
Series is similar to numpy array.<br>
The major difference between Series and list is in Series we can change the index to any number or string.<br>
If we want to retrive any value from Series we need call the label of the element that is it's index name
> g7_pop['Canada'] *This works similar to dictionaries*

We can still return elements by using number but we have to use *iloc* attribute
>g7_pop.iloc[0] * this will return first element of the Series*

We can alos select multiple elements which we did in numpy by passing list of index
>g7_pop[['Italy','France']]
g7_pop.iloc[[0,1]]
*This will return another Series*

We can perform operation of vectorization and boolean arrays which we did in numpy but can also do in series.<br>
>gz_pop[(g7_pop>80)&{g7_pop<200)] *this will retrunseries population which is greater than 80 and less than 200*

Dataframe is collection of multiple Series.<br>
We can assign index value and column value similarly to we did in Series foir index.<br>
We can get summary statstics of every numberic column.<br>
>df.describe()

To select any row from Dataframe we can use *loc* and *iloc* attributes.
For loc we need to pass index labels in the list
>df.loc['Canada'] *this will return Series containing information related to Canada*

For iloc we need to pass position number for example -1 as last row or 5 for 6th row
>df.iloc[-1] *this will return Series containing information realted to United States*

df['Something'] will return that named column.<br>
We can do all operation we did in numpy for example we can do slicing, and we can put multiple dimension.<br>
For droping the element do df.drop('Canada') it will drop Canada and return the remaining Dataframe. But it will not drop it from the actual dataframe.<br>
Like in numpy we can perform multiple operations. Also by passing multiple columns as list we can do operation on more than one table together.
>df[['Population', 'GDP']] / 100

For making new columns we can make series related to that columns and give index value as that of dataframe.<br>
We can also rename the index and columns.<br>
>df.rename(
    columns={
        'HDI': 'Human Development Index',
        'Anual Popcorn Consumption': 'APC'
    }, index={
        'United States': 'USA',
        'United Kingdom': 'UK',
        'Argentina': 'AR'
    })
    
We can also perform string operation on index labels. Like *str.upper* using the rename function.<br>
For dropping the columns permentaley we can do inplace value true for that column<br>
>df.drop(columns='Language', inplace=True)

Making new column from the existing columns
>df['GDP Per Capita'] = df['GDP'] / df['Population']

# Part 5
The only thing you need to do is just use methods like isnull and fillna/dropna and pandas will take care of the rest.<br>
Taking a look at the column, we can see that Pandas filled in the blank space with “NA”. Using the isnull() method, we can confirm that both the missing value and “NA” were recognized as missing values. Both boolean responses are True. <br>
This is a simple example, but highlights an important point. Pandas will recognize both empty cells and “NA” types as missing values.<br>
Usually, for a "categorical" type of field (like Sex, which only takes values of a discrete set ('M', 'F')), we start by analyzing the variety of values present. For that, we use the unique() method:
>df['Sex'].unique()

We can replace D with F
>df['Sex'].replace('D', 'F')

"duplicated" means "all the column values should be duplicates". We can customize this with the subset parameter:<br>
You know that the single columns represent the values "year, Sex, Country and number of children", but it's all been grouped in the same column and separated by an underscore. Pandas has a convenient method named split that we can use in these situations:
>df['Data'].str.split('_')

#Part 6 
we can give the title to any matpotlib *plt.title()*.<br>
plt.plot(x,y)
we can plot any line 
>plt.plot(x, x ** 2), 
plt.plot(x, -1 * (x ** 2))

>set_xlabel() *we can label x axis*<br>
axes.set_ylabel() *we can set y axis to any name*
** linestyle='solid'
**  linestyle='dashed'
** linestyle='dashdot'
** linestyle='dotted'
<br>
When we call the subplots() function we get a tuple containing a Figure and a axes element.<br>
We can also define how many elements we want inside our figure. To do that we can set the nrows and ncols params.
>plot_objects = plt.subplots(nrows=2, ncols=2, figsize=(14, 6))

fig, ((ax1, ax2), (ax3, ax4)) = plot_objects

plot_objects

>plot(x,y)<br>
scatter(x,y)<br>
bar(x,height)<br>
stem(x,y)<br>
step(x,y)<br>
stackplot(x,y)

# Part 7
When you want to work with a file, the first thing to do is to open it. This is done by invoking the open() built-in function.

open() has a single required argument that is the path to the file and has a single return, the file object.

The with statement automatically takes care of closing the file once it leaves the with block, even in cases of error.

>filepath = 'btc-market-price.csv'

with open(filepath, 'r') as reader:
    print(reader)
    
 first method we'll learn is read_csv, that let us read comma-separated values (CSV) files and raw text (TXT) files into a DataFrame.
 ** filepath: Path of the file to be read.
 We can define a na_values parameter with the values we want to be recognized as NA/NaN. In this case empty strings '', ? and - will be recognized as null values.
 df = pd.read_csv('btc-market-price.csv',
                 header=None,
                 na_values=['', '?', '-'])
 We'll add that columns names using the names parameter.
 Without using the dtype parameter pandas will try to figure it out the type of each column automatically. We can use dtype parameter to force pandas to use certain dtype.










