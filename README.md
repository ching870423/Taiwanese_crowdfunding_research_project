# Taiwanese_crowdfunding_research_project
Implementation for long-term development of Taiwanese crowdfunding from big data perspective.

## Background
Workinsa as a Data Science research assistant at Academia Sinica, I teamed up with [Szu-Chuang Li](http://www.ic.tku.edu.tw/index.php/component/sppagebuilder/page/50-tommy.html) to conduct an innovative research: A Study of the Project Trends on Taiwanese Crowdfunding Platforms.

In the research project, I extracted, transformed and loaded a collection of text & numerical data on 2 major crowdfunding platforms in Taiwan. I also processed textual descriptioin and performed keywords extraction in text mining to determine popular topics among fundraising ventures from 2012-2020. The statistical findings and the trend of crowdfunding projects could generate insights for start-up firms requiring to raise funding for running business in Taiwan.

The research findings are 
1. In 2018, Zeczec surpassed Flying-V as the leading crowdfunding platform in Taiwan, while projects on Flying-V receive more funds on average.
2. Crowdfunding projects in technology and design perform better in Taiwan. Popular categories such as gaming and media production do not perform well as they do on Kickstarter.
3. The use of rich media like images and videos grows over time, which is expected.
4. Some keywords are frequently used in project descriptions but do not necessarily bring more income for the projects.

## Project Structure
Overall, Python is the main language for implementation and the result is run on Jupyter Notebook platform. For the extraction part, I only present the sample code for the Zeczec websites.

In the file, [01_webcrawler_zeczec_to_mysql.ipynb](https://github.com/ching870423/Taiwanese_crowdfunding_research_project/blob/main/01_webcrawler_zeczec_to_mysql.ipynb), using [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/) to load the html code on crowdfunding websiates and formating the required information, such as project_name, category, description..., into table. Then, I loaded the information into MySQL database built-in XAMPP on local side. 3577 crowdfunding projects on Zeczec are collected, and can be modified to gather similar information on the FlyingV platform.

In the file, [02_extract_description_zec.ipynb](https://github.com/ching870423/Taiwanese_crowdfunding_research_project/blob/main/02_extract_description_zec.ipynb), I extracted textual description from origin html source and from images using [Google Vision API](https://cloud.google.com/vision/docs/ocr).

In the file, [03_zec_ckipcut_wordcloud.ipynb](https://github.com/ching870423/Taiwanese_crowdfunding_research_project/blob/main/03_zec_ckipcut_wordcloud.ipynb), I tokenized the words in description of each crowdfunding projects by [CkipTagger](https://github.com/ckiplab/ckiptagger), which could preformance well in traditional Chinese corpus. The tokenized corpus of each projects would be stoared into MySQL database as well. Then, I visulized the popular words into word clouds using library [WordCloud](https://pypi.org/project/wordcloud/) after cleaning stopwords for merging all project description as a corpus. Belows is an example, [zeczec_wordcloud_v2.png](https://github.com/ching870423/Taiwanese_crowdfunding_research_project/blob/main/zeczec_wordcloud_v2.png).

![zeczec_wordcloud_v2](https://user-images.githubusercontent.com/66129087/140638891-fde10687-4fbf-48e1-8b16-f33c557d03d5.png)

In the file, [04_keyword_tfidf_year.ipynb](https://github.com/ching870423/Taiwanese_crowdfunding_research_project/blob/main/04_keyword_tfidf_year.ipynb), I performed TF-IDF  and selected the first 100 terms with high TF-IDF weights for each project's description. Then, I determined the popular keywords by counting the occurence of these terms and exported the result of each year into a csv file. An example of 2020 is in the file, [zeczec_2020_top_keyword_tfidf.csv](https://github.com/ching870423/Taiwanese_crowdfunding_research_project/blob/main/zeczec_2020_top_keyword_tfidf.csv). Below is the example result of Zeczec platorms in traditional Chinese. The terms in the table are top 3 keywords that are used in project description frenquently. Most of them related to mobile phone, charging, and gaming.

|year/ranking|2018|2019|2020|
|---|---|---|---|
|1|遊戲|收納|充電|
|2|玩家|充電|手機|
|3|音樂|遊戲|收納|

In the file, [05_topkeyword_price.ipynb](https://github.com/ching870423/Taiwanese_crowdfunding_research_project/blob/main/05_topkeyword_price.ipynb), I figured out the keywords that might bring more fundings. The method I implemented is to add up the funding price based on the top keyword I explored before and to sortthe terms according to the amount of fundings. Below is the keywords with the most fundings in traditional Chinese.

|year/ranking|2018|2019|2020|
|---|---|---|---|
|1|台灣人|清洗|模式|
|2|矽膠|矽膠|自動|
|3|內建|專利|智慧|
