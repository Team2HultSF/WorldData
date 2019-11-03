# importing packages
import pandas as pd  # data science essentials
import matplotlib.pyplot as plt  # data visualization
import seaborn as sns  # more data visualization
import time
import sys

def import_data():
    global world_data  # this makes the world data that has been created as a global variable
    # Select the data file you would like to access
    file = input('Which file would you access? Please make sure to add .xlsx at the end \n')
    # Reads it as a DataFrame
    world_data = pd.read_excel(file)
    section_selection()


def section_selection():
    global section_selection
    # Determine the area/reagion you would like to analyze
    section_selection = input('Which Transformer region would you like to analyze? \n')
    print(f'Are you sure you want to analyse for {section_selection} ?')
    yes_no = input('(Yes/No)')
    # Just a
    while yes_no in ['No', 'N', 'no', 'n']:
        section_selection = input(
            'Which transformer region would you like to analyze? \nIf you make a mistake, the code needs to re-run :(')
        print(f'Are you sure you want to analyse for {section_selection} ?')
        yes_no = input('(Yes/No)')
    if yes_no in ['Yes', 'yes', 'y', 'n']:
        selection = world_data[world_data ['Cool Name'] == 'Hot Rod']
        print(selection.info())
        # analysis_choice()
    else:
        print('Something went wrong')
        choice1 = input('Would you like to try to analyse the data again? \n(y/n)')
        while choice1 not in ['y','n']:
            choice1 = input('Would you like to try to analyse the data again? \n(y/n)')
        if choice1 == 'y':
            section_selection()
        elif choice1 == 'n':
            exit()
        else:
            print('404')

# def analysis_choice():
import_data()

import pandas as pd
import numpy as np
import seaborn as sns
world_data = pd.read_excel('WDIW Dataset.xlsx', index_col = 'Country Name',
                              na_values= ' ')
missing_data = pd.read_excel('After missing data ver.1.xlsx', sheet_name = 'final dataset', index_col = 'Country Name')
s = world_data[world_data ['Cool Name'] == 'Hot Rod']
s1 = s.iloc [0:1
             ,1]
print (s1)
s = s.drop(['Cool Name', 'Hult Region','Country Code'], axis = 1)
s = s.drop(['Bermuda'])
print(s.shape)
print(missing_data.shape)
print(s.isnull().sum().sum())
final_dataset = pd.merge(s,missing_data)
print (final_dataset.shape)
print(final_dataset.isnull().sum().sum())
final_dataset1 = final_dataset.dropna(axis=1,how='all')
print (final_dataset1.shape)
education = ['Age dependency ratio (% of working-age population)', 'Age dependency ratio, old (% of working-age population)'
 , 'Age dependency ratio, young (% of working-age population)' , 'GDP (current US$)' , 'GDP growth (annual %)' , 'Industry (including construction), value added (% of GDP)' ,
             'Agriculture, forestry, and fishing, value added (% of GDP)' , 'Merchandise trade (% of GDP)' , 'Military expenditure (% of GDP)' , 
             'Services, value added (% of GDP)' , 'Population ages 15-64 (% of total population)' , 'Population ages 65 and above (% of total population)' , 'Population density (people per sq. km of land area)' , 
             'Population growth (annual %)' , 'Employment in services (% of total employment) (modeled ILO estimate)' , 'Population, total',
             'Unemployment rate (%)' , 'Education Expenditure (M.$)' , 'Education Expenditure (%GDP)']
education_dataset = final_dataset1.loc[: , education]
print (education_dataset.shape)
education_corr = education_dataset.corr().round(2)

sns.heatmap(data       = education_corr,
            cmap       = 'Blues',
            square     = True,
            annot      = False,
            linecolor  = 'black',
            linewidths = 0.5)
plt.show()
