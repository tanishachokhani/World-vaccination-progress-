# World-vaccination-progress-
# Importing_libraries 
import numpy as np 
import pandas as pd 
import matplotlib.pyplot as plt 
import seaborn as sns 
from sklearn.impute import SimpleImputer
import plotly.express as px
%matplotlib inline 
#Importing_data 
Vaccinations= pd. read_csv('country_vaccinations-4.csv')
Vaccinations.head(40)

# Exploratory_data _analysis
Vaccinations.info()

# Finding missing_values 
sns.heatmap(Vaccinations.isnull(),yticklabels=False,cbar=False,cmap='viridis')
# Deleting the null_values 
Vaccinations_na=Vaccinations.dropna()
Vaccinations_na.head(40)

# Printing headcount_of_countries and vaccines in the dataset
print('Total no of countries in the data set ',len(Vaccinations_na.country.unique()),'\n')
print('Total no of unique vaccines in the data set ',len(Vaccinations_na.vaccines.unique()),'\n')

Country= Vaccinations_na.country.unique()
date = Vaccinations_na.date.str.split('-',expand =True)
date
# Formatting the data 
Vaccinations_na['year'] = date[0]
Vaccinations_na['month] = date[1]
Vaccinations_na['day'] = date[2]
Vaccinations_na.year = pd.to_numeric(Vaccinations_na.year)
Vaccinations_na.month = pd.to_numeric(Vaccinations_na.month)
Vaccinations_na.day = pd.to_numeric(Vaccinations_na.day)
Vaccinations_na.date = pd.to_datetime(Vaccinations_na.date)
Vaccinations_na.head()

# Grouping the data 
total_by_country=Vaccinations_na.groupby('country')['vaccines'].value_counts()
total_by_country.head(40)
df = pd.DataFrame(total_by_country,columns= 'country vaccines total'.split())
df.head()
df.columns =['null', 'total','null2']
df.head()
df1= df.drop(['null','null2'], axis = 1)

total_vaccine=df1.groupby('vaccines')['total'].value_counts()
total_vaccine.head()
total_vaccine.describe()

vaccinations_daily=Vaccinations_na.groupby('country')['daily_vaccinations'].sum()
vaccinations_daily.head()

# Visualisations
sns.heatmap(df.corr())
plt.title('Corelation Heatmap')
plt.yticks(rotation = 0);
size(10,7)
![Screen Shot 2021-04-12 at 9 32 33 PM](https://user-images.githubusercontent.com/82114061/114426366-a301a500-9bd7-11eb-9076-78ea33963247.png)

fig = px.line(df, x = 'date', y ='daily_vaccinations', color = 'country')

fig.update_layout(
    title={
            'text' : "Daily vaccination trend",
            'y':0.95,
            'x':0.5
        },
    xaxis_title="Date",
    yaxis_title="Daily Vaccinations"
)

fig.show()
![Screen Shot 2021-04-12 at 9 32 33 PM](https://user-images.githubusercontent.com/82114061/114426634-e3612300-9bd7-11eb-882a-1f4a23c29b7a.png)

# Plotting a line_graph
fig = plt.figure()
ax = fig.add_axes([0,0,1,1])
y_axis= [647950,5689294,2103641,67279288,10251871,963107,57272,11398790,7573761,35300572,151286560]
x_axis = ['Australia','Canada','China','India','Italy','Japan','NZ','Russia','UAE','UK','US']
plt.plot(x_axis,y_axis,color='green', linestyle='dashed', linewidth = 3,
         marker='o', markerfacecolor='blue', markersize=12)
plt.title('Daily vaccinations')
plt.ylabel('Vaccinations')
plt.savefig('Daily vaccinations.png')
plt.show()
![image](https://user-images.githubusercontent.com/82114061/114319330-9c6b2300-9b2e-11eb-916a-1503b51a92e1.png)

x_axis=['Canada','India','Italy','Japan','NZ','Russia','UAE','UK','US']
y_axis=People_vaccinated=[148080561,1413018974,258975685,10075536,150744,144082865,4316983,1408451181,3918260669]
plt.plot(x_axis,y_axis,color='grey', linestyle='--', linewidth = 3,
         marker='o', markerfacecolor='blue', markersize=12)
plt.title('People Vaccinated')
plt.ylabel('Vaccinations')
plt.xlabel('Country')
plt.savefig('People Vaccinated.png')
plt.show()
![image](https://user-images.githubusercontent.com/82114061/114319398-071c5e80-9b2f-11eb-80a5-ad08b15b202d.png)

x_axis=['Canada','India','Italy','Japan','NZ','Russia','UAE','UK','US']
y_axis=[31024007,236896324,117044867,881104,16483,63424077,2437849,101444983,1824732019]
plt.plot(x_axis,y_axis,color='grey', linestyle='--', linewidth = 3,
         marker='o', markerfacecolor='blue', markersize=12)
plt.title('People Fully Vaccinated')
plt.ylabel('Vaccinations')
plt.xlabel('Country')
plt.savefig('People fully Vaccinated.png')
plt.show()
![image](https://user-images.githubusercontent.com/82114061/114319410-156a7a80-9b2f-11eb-9c8b-bc8e08f23e85.png)


x1 = ['Canada','India','Italy','Japan','NZ','Russia','UAE','UK','US']
y1 = [148080561,1413018974,258975685,10075536,150744,144082865,4316983,1408451181,3918260669]
plt.plot(x1, y1, label = "People Vaccinated")
x2 = ['Canada','India','Italy','Japan','NZ','Russia','UAE','UK','US']
y2 = [31024007,236896324,117044867,881104,16483,63424077,2437849,101444983,1824732019]
plt.plot(x2, y2,label = "People Fully Vaccinated")
plt.xlabel('Country')
plt.ylabel('Vaccinations')
plt.title('People Vaccinated VS People Fully Vaccinated')
plt.legend()
plt.show()
![image](https://user-images.githubusercontent.com/82114061/114319417-1d2a1f00-9b2f-11eb-9811-e97f9183814c.png)

# Data_sorting & Plotting a bar_chart
single_vaccine = Vaccinations['vaccines'].value_counts()
single_vaccine = single_vaccine[['Oxford/AstraZeneca', 
                                 'Pfizer/BioNTech', 
                                 'Sputnik V', 
                                 'Sinopharm/Beijing',
                                 'Sinovac', 
                                 'Johnson&Johnson', 
                                 'Moderna']]
single_vaccine.head()

background_color = "#f6f5f5"
color_map = ["lightgray" for _ in range(7)]
color_map[1] = "#2693d7"
sns.set_palette(sns.color_palette(color_map))

plt.rcParams['figure.dpi'] = 300
fig = plt.figure(figsize=(5, 2), facecolor='#f6f5f5')
gs = fig.add_gridspec(1, 1)
gs.update(wspace=0, hspace=0)
ax0 = fig.add_subplot(gs[0, 0])
ax0.set_facecolor(background_color)

ax0.tick_params(axis = "y", which = "both", left = False)
ax0.text(0, -1, 'Most used vaccine across countries', color='black', fontsize=7, ha='left', va='bottom', weight='bold')
ax0.text(0, -0.93, 'Pfizer/BioNTech is the most popular single vaccine', color='black', fontsize=5, ha='left', va='top')
ax0_sns = sns.barplot(ax=ax0, y=single_vaccine.index, x=single_vaccine, zorder=2, orient='h', linewidth=0.3, edgecolor='black')
ax0_sns.set_xlabel("Number of Countries",fontsize=5, weight='bold')
ax0_sns.set_ylabel("Vaccine",fontsize=5, weight='bold')
ax0_sns.tick_params(labelsize=5)
plt.show()
![image](https://user-images.githubusercontent.com/82114061/114319265-6463e000-9b2e-11eb-80d3-7e31c4ed287d.png)

# Plotting using geographical_plotting- choropleth map 
data=pd.read_csv('countrywise_data.csv')
import geopandas as gp
from shapely.geometry import Point
import plotly.express as px
tdf = data.copy()

fig = px.choropleth(tdf,                            
    locations="Country_name",           
    color="Daily_Vaccinations",                     
    hover_name="People_vaccinated",              
    animation_frame="People_fully_vaccinated",
    color_continuous_scale= 'magma',
    projection="natural earth",       
    range_color=[0,12],
    title='<span style="font-size:36px; font-family:Times New Roman">Number_of_vaccinations per country</span>')                
fig.show()
![image](https://user-images.githubusercontent.com/82114061/114319253-5c0ba500-9b2e-11eb-9993-45641170d86b.png)




# Observations
1.Though the vaccination drive is going in its full pace but in most of the countries people are not fully vaccinated
2.In North America and Europe Pfizer and Moderna is widely used
3.The most used vaccine around the world is Pfizer/ BioNTech. Around 47.6% of the total vaccines used
Indian Covaxin, Oxford/AstraZeneca comes at 10th with 0.933% market share.
4.Though USA started in the second position but in terms of daily vaccinations USA is at the top now
