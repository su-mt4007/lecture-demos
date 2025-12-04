# Week 5


## Example of JSON

``` {json}
{
    "username" : "taariqnazar",
    "friends" : ["taariq friend 1", "taariqs friend 2"]
}
```

## Example of XML

``` {xml}
<username>
taariqnazar
</username>
<friends>
    <friend>
        ...
    </friend>
    <friend>
        ...
    </friend>
</friends>
```

# Retrieving data from REST API

``` python
import requests 

response = requests.get("https://cataas.com/api/cats?tags=cute")
data = response.json()

print(data)
```

    [{'id': '0F0IKAPOdWiE755P', 'tags': ['meet', 'cute'], 'mimetype': 'image/jpeg', 'createdAt': '2024-06-18T09:46:45.702Z'}, {'id': '0GC9MRUAqxhBzPyA', 'tags': ['cute'], 'mimetype': 'image/png', 'createdAt': '2024-09-15T15:45:25.375Z'}, {'id': '0mstmOIucwiN80jb', 'tags': ['cute', 'black'], 'mimetype': 'image/jpeg', 'createdAt': '2023-10-25T00:04:03.771Z'}, {'id': '0RU7ZkgzyvWv8UJG', 'tags': ['tuxedo', 'computer', 'sleepy', 'cute', 'sleeping'], 'mimetype': 'image/png', 'createdAt': '2024-04-20T22:52:58.132Z'}, {'id': '0ztFbDrgDV2K7yJ1', 'tags': ['cute', 'orange', 'funny', 'lasagna', 'garfield'], 'mimetype': 'image/jpeg', 'createdAt': '2024-08-23T20:15:26.393Z'}, {'id': '1bJraW0IwSPm3MVd', 'tags': ['cute', 'fluffy'], 'mimetype': 'image/jpeg', 'createdAt': '2022-04-27T01:49:50.792Z'}, {'id': '1CF7xZmlX0t8QpgP', 'tags': ['ange', 'cute'], 'mimetype': 'image/jpeg', 'createdAt': '2016-11-22T05:38:06.656Z'}, {'id': '1DrcyohjhwcNaRIz', 'tags': ['cute', 'orange', 'sleepy', 'tired', 'outside', 'grass'], 'mimetype': 'image/jpeg', 'createdAt': '2024-02-29T00:49:57.420Z'}, {'id': '1KeQpy7eHqi0SFmc', 'tags': ['orange', 'cute', 'lying', 'bed', 'blanket'], 'mimetype': 'image/jpeg', 'createdAt': '2024-10-08T23:54:00.959Z'}, {'id': '1N2AH31jiY6N9TYc', 'tags': ['cute', 'mlem'], 'mimetype': 'image/jpeg', 'createdAt': '2024-02-08T07:59:29.085Z'}]

# Web scraping

``` python
from bs4 import BeautifulSoup as bs

response = requests.get("https://books.toscrape.com/")
html = response.text

soup = bs(html, "html.parser")

section = soup.find("section")
lis = section.find_all("li")

for li in lis:
    # Title → <h3><a title="..."></a></h3>
    a_tag = li.select_one("h3 a")
    title = a_tag.get("title") if a_tag else None

    # Price → <p class="price_color">£...</p>
    price_tag = li.select_one("p.price_color")
    price = price_tag.get_text(strip=True) if price_tag else None

    print(title, price)
```

    A Light in the Attic Â£51.77
    Tipping the Velvet Â£53.74
    Soumission Â£50.10
    Sharp Objects Â£47.82
    Sapiens: A Brief History of Humankind Â£54.23
    The Requiem Red Â£22.65
    The Dirty Little Secrets of Getting Your Dream Job Â£33.34
    The Coming Woman: A Novel Based on the Life of the Infamous Feminist, Victoria Woodhull Â£17.93
    The Boys in the Boat: Nine Americans and Their Epic Quest for Gold at the 1936 Berlin Olympics Â£22.60
    The Black Maria Â£52.15
    Starving Hearts (Triangular Trade Trilogy, #1) Â£13.99
    Shakespeare's Sonnets Â£20.66
    Set Me Free Â£17.46
    Scott Pilgrim's Precious Little Life (Scott Pilgrim #1) Â£52.29
    Rip it Up and Start Again Â£35.02
    Our Band Could Be Your Life: Scenes from the American Indie Underground, 1981-1991 Â£57.25
    Olio Â£23.88
    Mesaerion: The Best Science Fiction Stories 1800-1849 Â£37.59
    Libertarianism for Beginners Â£51.33
    It's Only the Himalayas Â£45.17
    None None
    None None
