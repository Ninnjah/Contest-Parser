# Animal Contest vote cheat

![Banner](https://github.com/Ninnjah/Contest-cheat/blob/master/banner.JPG)

It's a little program need for cheat votes for a child animal contest(i've coded it for my sister).

It's possible because website check only your ip address for voting, and i used a socks5 proxy servers to bypass protection [contest](https://stolicadetstva.com/competition/work/277/)
Actually this program just send request using a proxy server from proxy list
# Functions
0. Cheat voting for "vote id"
  ```python
  url = 'example-website.com'
  ip = ['proxy ips from .txt file']
  
  requests.get(url, proxies=dict(http = 'socks5://'+ip, https = 'socks5://'+ip))
  ```
1. Cheat voting with Tor
  
2. Generating proxy ip list from html file of 'http://spys.one/proxies/'
  ```python
    with open('socks.html', encoding='utf-8') as f: 
        html = f.read()                              
    proxyfile = open('proxy.txt', 'w')              
    soup = BeautifulSoup(html, 'html.parser')     
    for script in soup.find_all('script'):
        script.extract()                            
    for i in soup.find_all('tr', 'spy1xx'):          
        ips = i.find_next('font','spy14')              
        if ips not in content:                       
            print(ips.get_text() + ':1080')
            print(ips.get_text() + ':1080', file=proxyfile)# Запись ip в файл
  ```
 3. Deleting list of used proxy ips(just in case)
  ```python
        try:
            os.remove('usedproxy.txt')
        except:
            print('Already deleted..')
            time.sleep(2)
  ```
  4. Collecting information about contest members
  ```python
  for i in lots:                                        
        member = i.find('p', 'who').get_text()                
        votes = i.find('p', 'compe_comment').get_text()       
        votes = votes.replace(' | Голосую', '')              
        votes = int(votes.replace('Голосов: ', ''))       
        try:                                                 
            link = i.find(text='Голосую').parent.get('href')   
            link = link.replace('/competition/vote/', '')      
            link = link.replace('/', '')                        
        except AttributeError:                                
            link = lang.get('outlinkMembers')
        if not link in allready or link == lang.get('outlinkMembers'):
            allready.append(link)                     
            member = link + ': ' + member                   
            memDict = {member : votes}                 
            membersDict.append(memDict)                         
            members += 1                                        
            print(tui.updScore(lang.get('memMembers'), members, 0), end='\r')
  ```
  5. Open contest website
  ```python
            tui.ul(['"Мохнатые, пернатые" - 277'])
            contest = input('Введи номер конкурса: ') 
            if contest.isnumeric() and len(contest):
                url = 'https://stolicadetstva.com/competition/work/' + contest
                webbrowser.open(url, new=0, autoraise=True)
  ```
# Screenshot of the website
![](https://github.com/Ninnjah/animalContest/blob/master/contestWebsite.png)

---
># Additional info
>## easyTui
>[easyTui](https://github.com/Ninnjah/easyTui) it's my module for easy TUI in my programs
>## Alpha version   NO MORE UPDATES
>this is my first version of this cheat. It's uses a Tor browser with subprocess module. It's bad but it my first program
>```python
>for i in range(n):
>    x = 0
>    while x < len(links):
>        #tor.open_new_tab(links[x-1])
>        tor.open_new_tab('https://stolicadetstva.com/competition/vote/47714/')
>        x += 1
>        time = random.randint(50,65)
>        while time > 0:
>            tui.updatingScore('До закрытия браузера', time, 1)
>            time -= 1
>        subprocess.run(['TASKKILL', '/F', '/IM', 'firefox.exe'], stdout=subprocess.DEVNULL)
>        classi += 1
>        print('\a', end = '')
>```
