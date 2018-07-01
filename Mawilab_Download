from bs4 import BeautifulSoup
from urllib.request import urlopen
import re
import requests
import bs4   
import os

html_page = urlopen("http://www.fukuda-lab.org/mawilab/v1.1/")
soup = BeautifulSoup(html_page,"lxml")
links = []

for link in soup.findAll('a', attrs={'href': re.compile("^20.*.html")}):
    links.append("http://www.fukuda-lab.org/mawilab/v1.1/"+link.get('href'))
    
print(links)

for lik in links:
    print("lik",lik)
    html_page = urlopen(lik)
    soup = BeautifulSoup(html_page,'html.parser')
    linkss = []
    
    for link in soup.findAll('a', attrs={'href': re.compile("^.*/.*/")}):
        linkss.append(link.get('href'))
        print("linkss",linkss)
        for url  in linkss:
            sites = "http://www.fukuda-lab.org/mawilab/v1.1/"+str(url)
            html = requests.get(sites)
            soup = bs4.BeautifulSoup(html.text, "html.parser")
            for link in soup.find_all('a', href=True):
                href = link['href']
                if any(href.endswith(x) for x in ['.csv']):
                    remote_file = requests.get(sites + href) 
                    with open(str(href),"wb") as pdf:
                        for chunk in remote_file.iter_content(chunk_size=1024):
                            if chunk:
                                pdf.write(chunk)
