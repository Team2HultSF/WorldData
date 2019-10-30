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
