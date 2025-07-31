Crypto Dashboard Web Application
Table of Contents

Overview
Features
Demo
Technologies Used
API Integration
Local Development Setup
Deployment (Prerequisites , Web Server Configuration, GitHub Pages setup)
DOCKER DEPLOYMENT
Challenges and Solutions
Credits and Acknowledgments
1. OVERVIEW                                                                                                                                                            Crypto Dashboard is a comprehensive web application designed to help users track and analyze cryptocurrency market trends in real time. It fetches live data from external APIs to display updated prices, recent news, and historical charts for major cryptocurrencies like Bitcoin, Ethereum, and others.                                                                                                                                                                                                         Built with modern web technologies, the dashboard provides an intuitive and responsive interface that caters to both beginner investors and experienced crypto traders. Its features include:

🔁 Real-time price updates

📰 Latest cryptocurrency news

📈 Historical performance graphs

📊 Market summaries and trends

🔐 Secure and API-driven architecture

Whether you're casually browsing or actively trading, Crypto Dashboard provides a reliable window into the dynamic world of digital assets.
⚠️Important Disclaimer                                                                                                                                                 This application is for educational and informational purposes only. The data displayed is sourced from third-party APIs and may not always be accurate or up to date. Crypto Dashboard does not provide financial, investment, or trading advice.                                                                                                                                                                                                                                                                   Users should always conduct their own research and consult with a professional financial advisor before making any investment decisions. The creators of this application are not responsible for any financial losses incurred as a result of using this tool.
✨ Features
Crypto Dashboard offers a robust set of tools for tracking and analyzing cryptocurrency markets:

🔄 Real-Time Price Updates
Live market data for major cryptocurrencies (e.g., BTC, ETH, LTC).

Fetched using trusted external APIs like CoinGecko or Alpha Vantage.

📰 Latest Crypto News
Aggregates news from reputable sources via APIs.

Keeps users informed about market trends and global crypto events.

📈 Historical Charts
Displays time-based performance graphs for selected coins.

Users can view data over multiple timeframes (1D, 7D, 1M, etc.).

💹 Market Overview
Visual summary of top gainers, losers, and market cap.

Data tables sortable by price, volume, and percent change.

🌐 Responsive UI
Optimized for desktop and mobile devices.

Built using modern web technologies like React, Tailwind CSS, and Chart.js.

⚙️API-Driven Architecture
Uses environment variables to manage API keys securely.

Clean separation between front-end logic and external services.
3. DEMO
A link to a demo video (demonstrating how to use application locally and how to access it online) : https://youtu.be/NJtoPtMzTKs

Open this link to access FitExplorer; http://web-01.yamal.tech or http://web-01.yamal.tech/home

4. Technology used:
Frontend: -HTML: for structuring a webpage -CSS: for styling -JavaScripts
API Interactions:
ExerciseDB API from https://rapidapi.com/justin-WFnsXH_t6/api/exercisedb
Deployment: Deployed on nginx on web-01 server and github pages
5. API INTERACTION
The application integrates with the ExerciseDB API from RapidAPI to access a comprehensive database of exercises. This API provides:

Complete exercise information including names, target muscles, body parts, and equipment 
High-quality demonstration GIFs for each exercise
Structured data for easy filtering and categorization
Real-time access to the latest exercise database
API Documentation: ExerciseDB API Documentation

6. LOCAL DEVELOPMENT SETUP
Follow these steps to set up the project for local development: Step 1: Clone this repo: FitExplore. by:

git clone https://github.com/rcyubahiro/
then move inside it by:

cd FitExplore

Step 2: OPEN THE PROJECT: You can simply open the index.html file in your browser as this is a purely front-end application

7. DEPLOYMENT
7.1 Prerequisites

only one web server:

Web-01 (where nginx is installed, and I configured /etc/nginx/sites_available/default, this file is where I hosted my application for instance: I put all my files used to make application including; HTML, CSS, and JS, all were put inside this /var/www/html so that it can be accessed by simply visiting the IP_Address of web-01)

GitHub Pages:

Application is also alternatively, deployed on github pages as it's only way it can be deployed with HTTPS because load balancing with my servers couldn't work due to the issues with web-02 and lb-01 (Link to deployed app on GitHub Pages: https://stevenalu.github.io/fitexplorer/)
7.2 Domain name

A domain used, was created from DotTech domain where I used to link up with the IP_Address so if you vist my domain you will get the same by visiting via IP_Address.
8. DOCKER DEPLOYMENT

This section explains how the FitExplorer web application and load balancer are containerized, built, deployed, and tested using Docker.

Docker Hub Image Details The Docker images are publicly available on my Docker Hub Account https://hub.docker.com/r/stevenalu :

web-01: https://hub.docker.com/r/rcyubahiro/web_infra_lab-web-01/tags

web-02: https://hub.docker.com/r/rcyubahiro/web_infra_lab-web-02/tags

lb-01: https://hub.docker.com/r/rcyubahiro/web_infra_lab-lb-01/tags
Once you are in the root of this repo when you clone it where:

https://github.com/waka-man/web_infra_lab
Then:

docker pull rcyubahiro/web_infra_lab-web-01:latest
docker pull rcyubahiro/web_infra_lab-web-02:latest
docker pull rcyubahiro/web_infra_lab-lb-01:latest
How to Build: Instructions (Local) Follow this:

docker build -t rcyubahiro/web_infra_lab-web-01:latest -f web/Dockerfile ./web
docker build -t rcyubahiro/web_infra_lab-web-02:latest -f web/Dockerfile ./web
docker build -t rcyubahiro/web_infra_lab-lb-01:latest -f lb/Dockerfile ./lb
Run Instructions (on Web01 & Web02) SSHed into each web server and ran:

docker pull rcyubahiro/web_infra_lab-web-01:latest  # on web-01
docker pull rcyubahiro/web_infra_lab-web-02:latest  # on web-02

docker run -d -And after i hasd to reload haproxy inside lb-01 after SSHed into it:

sudo service haproxy restart
Testing steps & evidence From my host machine, I repeatedly ran:

curl -i http://localhost:8082

Screenshot below shows the live process and demo when FitExplorer application hosted on web-01 running on local machine: Screenshot 2025-07-27 001137 image

9. CHALLENGES AND SOLUTIONS
API Rate Limiting Challenge: RapidAPI imposes request limits on free tier accounts. solution: upgrading to a paid plan that could be solution in the future

10. CREDITS and ACKNOWLEDGEMENT
API USED:

https://www.alphavantage.co/documentation/

https://newsdata.io/documentation

https://docs.coingecko.com/reference/introduction

Visit the links above for it's documentation.-name rcyubahiro-web --restart unless-stopped -p 8080:8080 rcyubahiro/web_infra_lab-web-01:latest  # web-01
docker run -d --name rcyubahiro-web --restart unless-stopped -p 8080:8080 rcyubahiro/web_infra_lab-web-02:latest  # web-02
Load Balancer Configuration (on lb-01) I configured HAProxy (/etc/haproxy/haproxy.cfg) with:

global
    daemon
    maxconn 256

defaults
    mode http
    timeout connect 5s
    timeout client  50s
    timeout server  50s

frontend http-in
    bind *:80
    default_backend servers

backend servers
    balance roundrobin
    server web01 172.20.0.11:80 check
    server web02 172.20.0.12:80 check
    http-response set-header X-Served-By %[srv_name]
And after i has to reload haproxy inside lb-01 after SSHed into it:

sudo service haproxy restart
Testing steps & evidence From my host machine, I repeatedly ran:

curl -i http://localhost:8082

Screenshot below shows the live process and demo when FitExplorer application hosted on web-01 running on local machine: Screenshot 2025-07-27 001137 image

9. CHALLENGES AND SOLUTIONS
API Rate Limiting Challenge: RapidAPI imposes request limits on free tier accounts. solution: upgrading to a paid plan that could be solution in the future

10. CREDITS and ACKNOWLEDGEMENT
API USED:

https://www.alphavantage.co/documentation/

https://newsdata.io/documentation

https://docs.coingecko.com/reference/introduction

Visit the links above for it's documentation.
