# Kindlate failinimede saamine

Soovitatavalt kasutada pärast wget-i

files = glob.glob('get_website_text/learning_feelingstream_com/**/*',recursive=True) <- võtab kõik dokumendid mis on sellel veebilehel
Et muuta mis faile võetakse peab muutma directory lõpus olevaid tärne ja/või kaldkriipse.(html faili saamiseks pane lõppu /*.html)
Pärast seda on soovitatav andmeid puhastada.
Siin on üks näide.

html_files = []

for f in files: 
    if f.endswith('html'):
        html_files.append(f)

def get_content(htmlfile):
    html = open(htmlfile).read()
    soup = BeautifulSoup(html)
    [s.extract() for s in soup(['script', '[document]', 'head', 'title'])]
    visible_text = soup.getText(strip=False)
    return visible_text

results = []

for f in html_files:
    if not os.path.isdir(f):
        try:
            res = get_content(f)
            results.append(res)
        except Exception as e:
            print(e)


for idx, r in enumerate(results):
    with open(f'data/feelingstream/{idx}.txt', 'w') as fp:
        fp.write(r)
