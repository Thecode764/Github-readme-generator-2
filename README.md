# Github readme generator
Generate you own readme using github readme generator
## Start
- Copy this code in main.py file
```python
# Github readme generator
import requests

# You name. for example my name is artin karimi (a iranian name)
name = "Artin karimi"

# Summary. For example a developer
summary = "A developer"

# Interested. For example web development
interested = "Web development"

# Working. I currently working on project
working_on = "Github readme generator"

# Learning. What are you learning? django?
learning = "Django"

# Email. How to reach me. enter you email
email = "artin962354@proton.me"

# Username. You github username
username = "Thecode764"

# Pronouns. Male or female?
pronouns = "Male"

# Fun fact about you
fun_fact = "..."

# What you are know?
know = "python,c,cpp,wordpress"

# Discord id. You discord id
discord_id = "..."

# Wakatime username: You wakatime username. make sure you wakatime profile is public
wakatime = "Thecode764"

# Generate file
file = "README.md"

print("Generating ...")

url = f"https://api.github.com/users/{username}"

response = requests.get(url)

if response.status_code == 200:
    data = response.json()
    bio = data["bio"]
    public_repos = data["public_repos"]
    followers = data["followers"]
    following = data["following"]

out = f"""
<h1 align="center">{name}</h1>
<h3 align="center">{summary}</h3>

- 👋 Hi, I’m {name}


- 👀 I’m interested in **{interested}**

- ♾ I currently working on **{working_on}**

- 🌱 I’m currently learning **{learning}**

- 📫 How to reach me {email}

- 😄 Pronouns: {pronouns}

- 😎 Fun fact: {fun_fact}

- ℹ️ My Bio: | {bio} |

- 📂 I created {public_repos} public repositories

- 👤 My followers number is {followers}

- 👤 I follow {following} users

<h3 align="center">Tech stack</h3>
<img src="https://skillicons.dev/icons?i={know}">
<h3>Stats</h3>
<img src="https://github-readme-stats.vercel.app/api?username={username}&show_icons=true&theme=dracula">
<h3>Most used languages</h3>
<img src="https://github-readme-stats.vercel.app/api/top-langs/?username={username}&theme=dracula&langs_count=300">
<h3>Others</h3>
<img src="https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fgithub.com%2F{username}%2F&count_bg=%23000&title_bg=%23171717&icon=github.svg&icon_color=%23FFFFFF&title=Visits&edge_flat=false">
<img src="https://img.shields.io/github/followers/{username}">
<h3>Discord status</h3>
<!--Join to lanyard server for this-->
<img src="https://lanyard.cnrad.dev/api/{discord_id}">
<h3>Trophy</h3>
<img src="https://github-profile-trophy.vercel.app/?username={username}&theme=dracula">
<img src="https://streak-stats.demolab.com/?user={username}&theme=dracula">
<h3>Activity graph</h3>
<img src="https://github-readme-activity-graph.vercel.app/graph/?username={username}&bg_color=000&color=fff&line=00E676&point=fff&hide_border=true">

<img src="https://github-profile-summary-cards.vercel.app/api/cards/profile-details?username={username}&theme=dark">

<img src="https://github-profile-summary-cards.vercel.app/api/cards/stats?username={username}&theme=dark">

<img src="https://github-readme-stats.vercel.app/api/wakatime?username={username}&theme=dracula">
"""

write = open(file, "w+")

write.write(out)
```
**Please read the code comments. please dont change out variable data**

Variables:

`name`: You name for example my name is artin karimi (a iranian name)

`summary`: You summary for example a developer

`interested`: Interested in .... for example web development

`working_on`: I currently working on ...

`learning`: I currently learning ... .

`email`: How to reach me. my email: ...

`username`: You github username

`pronouns`: Male or female?

`fun_fact`: Fun fact: ...

`know`: What programming languages you are know?

`discord_id`: You discord id. Hmmmm notice: Github readme generator use lanyard widgets. please join the lanyard discord server

`wakatime`: you wakatime username

`file`: Generate file (README.md)

So create a file in `.github/workflows/readme.yml`
```yaml
name: Update readme
on:
  schedule: 
    - cron: '0 * * * *'
  workflow_dispatch:

permissions:
  contents: write

jobs:
  activity-update:
    name: Update activity
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      
      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.x'

      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install requests

      - name: Update with about me
        run: python main.py

      - name: Commit and push changes
        run: |
          git pull
          git config --global user.name "Github actions"
          git config --global user.email "actions@github.com"
          git add .
          git commit -m "Update README"
          git push
```

This action runs automatically at every hour