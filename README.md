# Taiwanese_crowdfunding_research_project
Implementation for long-term development of Taiwanese crowdfunding from big data perspective.

## Background
Workinsa as a Data Science research assistant at Academia Sinica, I teamed up with [Szu-Chuang Li](http://www.ic.tku.edu.tw/index.php/component/sppagebuilder/page/50-tommy.html) to conduct an innovative research: A Study of the Project Trends on Taiwanese Crowdfunding Platforms.

In the research project, I extracted, transformed and loaded a collection of text & numerical data on 2 major crowdfunding platforms in Taiwan. I also processed textual descriptioin and performed keywords extraction in text mining (tf-idf) to determine popular topics among fundraising ventures from 2012-2020. The statistical findings and the trend of crowdfunding projects could generate insights for start-up firms requiring to raise funding for running business in Taiwan.

The research findings are 
1. In 2018, Zeczec surpassed Flying-V as the leading crowdfunding platform in Taiwan, while projects on Flying-V receive more funds on average.
2. Crowdfunding projects in technology and design perform better in Taiwan. Popular categories such as gaming and media production do not perform well as they do on Kickstarter.
3. The use of rich media like images and videos grows over time, which is expected.
4. Some keywords are frequently used in project descriptions but do not necessarily bring more income for the projects.

## Project Structure
Overall, Python is the main language for implementation and the result is run on Jupyter Notebook platform.

In the file, [01_webcrawler_zeczec_to_mysql.ipynb](https://github.com/ching870423/Taiwanese_crowdfunding_research_project/blob/main/01_webcrawler_zeczec_to_mysql.ipynb), using [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/) to load the html code on crowdfunding websiates and formating the required information, such as project_name, category, description..., into table. Then, I loaded the information into MySQL database built-in XAMPP on local side. 3577 crowdfunding projects on Zeczec are collected, and can be modified to gather similar information on the FlyingV platform.

In the file, [02_extract_description_zec.ipynb](https://github.com/ching870423/Taiwanese_crowdfunding_research_project/blob/main/02_extract_description_zec.ipynb), I extracted textual description from origin html source and from images using [Google Vision API](https://cloud.google.com/vision/docs/ocr)/

In the file, [03_zec_ckipcut_wordcloud.ipynb](https://github.com/ching870423/Taiwanese_crowdfunding_research_project/blob/main/03_zec_ckipcut_wordcloud.ipynb), I cut the description of each crowdfunding projects
