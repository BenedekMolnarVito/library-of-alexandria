# Initialize Personal Vault based on the given information AND my OneDrive account

## GOAL

The goal of this task is to initialize the Personal Vault with the provided information about me, and with additional information fetched from my OneDrive account. This is my life and I want to use this Personal Vault to store and manage all my important information, documents, and data in a secure and organized manner. I want this Vault to be similarly structured as an already existing vault called *ai*. Keep in mind that these information is not from Obsidian, but the raw data that I want to use to initialize the Personal Vault has to be processed similarly to the *ai* vault, so it can be easily integrated and used within the Personal Vault.
These information is not static, it can be updated and changed over time, so the Personal Vault should be flexible and adaptable to accommodate any changes in my information or preferences.
**IMPORTANT**: The Personal Vault should be designed in a way that it can easily referenced by other llm-agents, so it should be structured and organized in a way that allows for easy access and retrieval of information by other agents. Also, it should be easy to integrate with other tools and applications that I use, such as my calendar, task manager, note-taking app, and other productivity tools. This will allow me to have a seamless and efficient workflow, and to easily access and manage all my information from one central location.
Save this prompt in the raw folder too.

## Information about me

### Personal information

- Name: Molnár Benedek
- Email: <molnar.benedictus@gmail.com>
- Country: Hungary
- City: Budapest
- Preferred language: English/Hungarian
- Preferred currency: HUF
- Preferred date format: YYYY-MM-DD
- Preferred time format: 24-hour
- Preferred time zone: Central European Time (CET)

### Professional information

- Occupation: Software Engineer
- Company: Madis Consulting Kft.
- Industry: Information Technology

Fetch more professional information about me from my OneDrive account (look for CVs, resumes, and other relevant documents) to further personalize the Personal Vault initialization process.

### My interests and hobbies

- TOP: AI and Agentic systems
- Technology and software development
- Traveling and exploring new cultures
- Ethymology and linguistics
- Runnning and outdoor activities
- Parkour and free running
- Stock market and investing
- Crypto trading and blockchain technology
- Fantasy and science fiction literature
- Video games and tabletop RPGs

### Information about my preferences and habits

- I prefer to use digital tools and applications for organization and productivity.
- I'm a bit ADHD, so I like to have a flexible and adaptable system that can accommodate my changing needs and preferences.
- I'm a generalist, so I like connecting the dots between different fields and topics, and I like to have a system that allows me to easily link and relate different pieces of information.

### Information about my stuffs

- My PC setup:
  1. CPU: AMD Ryzen 7 3700X 8-Core Processor
  2. GPU: AMD Radeon RX 5700 XT 8GB GDDR6
  3. RAM: 16GB DDR4
- My phone: POCO F5 with Xiaomi HyperOS 3.0.3.0
- My preferred web browser: Firefox
- My preferred code editor: Visual Studio Code
- My preferred Code-Assistant: GitHub Copilot
- My hobby server: A self-hosted server running on an old HP laptop, used for hosting personal projects, testing, and learning about server management and networking. My domain for the server is *vitoscaletta.duckdns.org*, and I use it to host some small web applications that I develop as part of my learning and experimentation with web development and server management. It is hosted by DuckDNS, the reverse proxy is nginx, and the apps are running on Docker containers. I also have 4TB NAS drive mounted on the server, which I use for storing and managing my files, media, and backups.
**IMPORTANT**: Sometime I want to SSH into my hobby server to access files, run commands, and manage my projects. When I ask an agent to SSH into my hobby server, it should be able to do so using this information
    1. LAN IP: 192.168.100.4
    2. Port: 22
    3. Username: (ASK FOR the username I use to access the server, which is not provided here for security reasons)
    4. Password: (ASK FOR the password I use to access the server, which is not provided here for security reasons)

## My OneDrive account

- Email: <molnar.benedictus@gmail.com>
- Storage capacity: 5 GB
- Location on my PC: *C:\Users\molna\OneDrive*

Scrape and fetch ALL information from my OneDrive account, such as documents, files, and other data that can be used to further personalize and initialize the Personal Vault. Note that this information is not static, it can be updated and changed over time, so the Personal Vault should be designed to accommodate any changes in the information stored in my OneDrive account. Also, it many documents are in Hungarian, so the Personal Vault should be able to process and understand information in both English and Hungarian languages. The Personal Vault should also be able to categorize and organize the information fetched from my OneDrive account in a way that allows for easy access and retrieval by other agents and tools that I use.
