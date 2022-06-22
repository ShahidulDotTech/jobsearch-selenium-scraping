import encodings
from selenium import webdriver
import pandas as pd
from selenium.webdriver.support.ui import WebDriverWait
import random
from selenium.webdriver.common.action_chains import ActionChains
from selenium.webdriver.common.keys import Keys
from time import sleep


path = 'D:\Softwares\Software\chromedriver\chromedriver.exe' # path to the web driver goes here
driver=webdriver.Chrome(path)
driver.maximize_window()
url = 'https://jobsearch.az/vacancies'
driver.get(url) # request the main url
driver.implicitly_wait(5) # wait till the main page loads

clicking = driver.find_element_by_xpath('//*[@id="scroller_desctop"]/div/div[1]/div/a/h3').click() # select all job title from main page
# scroll through the whole list to load
for r in range(0, 1):
    if r <=4:
        ActionChains(driver).send_keys(Keys.END).perform()
        sleep(random.uniform(1, 5))   

# make empty lists for the data
title = []
deadline = []
company = []
category = []

elements = driver.find_elements_by_xpath('//*[@id="scroller_desctop"]/div/div/div/a/h3') # select all job title from main page
# scrape all the element
for element in elements:
    element.click()
    sleep(random.uniform(1, 5))
    title.append(driver.find_element_by_class_name('vacancy__title').text.encode('utf-8').decode('ascii', 'ignore').strip()) # select job title from right panel
    deadline.append(driver.find_element_by_class_name('vacancy__deadline').text.encode('utf-8').decode('ascii', 'ignore').replace('Son tarix ', '').strip()) # select deadline from right panel
    company.append(driver.find_element_by_xpath('//*[@id="body-block"]/div/div[1]/div[1]').text.encode('utf-8').decode('ascii', 'ignore').strip()) # select company name from right panel
    category.append(driver.find_element_by_xpath('//*[@id="body-block"]/div/div[2]/span[2]/a').text.encode('utf-8').decode('ascii', 'ignore').strip()) # select category from right panel
    # views  = driver.find_element_by_xpath('/html/body/div/div/div/div/div[2]/div/div[2]/div[2]/div/div[1]/div/div/ul/li[2]/span').text # select views from main panel (it has a bug)
    print(title, deadline, company, category) # print the data

df = pd.DataFrame({'title': title, 'deadline': deadline, 'company': company, 'category': category}) # save the data to a dataframe
df.to_excel('jobserach.xlsx', index = False) # convert the dataframe to excel

driver.close()
