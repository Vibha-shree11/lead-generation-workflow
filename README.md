# Assignment 1: Lead Sniper - High Value GitHub Lead Tracker

## Project Overview
An automated workflow built with n8n that monitors GitHub 
repository stars and identifies high-value leads based on 
their follower count and public repositories.

## Tools Used
- n8n (workflow automation)
- GitHub API
- Discord Webhooks
- JavaScript (Code node)

## Workflow Steps
1. Schedule Trigger - runs every 5 minutes
2. HTTP Request - fetches latest stargazers from GitHub repo
3. HTTP Request - enriches each user's full profile
4. Filter - keeps only users with 100+ followers OR 50+ repos
5. Code Node - generates AI sales pitch from bio and company
6. HTTP Request - sends formatted message to Discord

## Filter Logic
- Followers > 100 OR Public Repos > 50 = High Value Lead
- Others are filtered out automatically

## AI Sales Pitch Logic
- If bio contains AI/ML keywords → AI focused pitch
- If bio contains Open Source → Developer focused pitch  
- If followers > 500 → Influencer focused pitch
- Otherwise → General engagement pitch

## Logic Log - GitHub API Rate Limits
GitHub API allows 60 requests per hour for unauthenticated 
requests. To handle this:
- Workflow runs every 5 minutes (not too frequent)
- Only fetches 5 stargazers per run (per_page=5)
- Uses Accept header: application/vnd.github.v3+json
- This keeps usage well within rate limits

## Sample Discord Output
🚨 NEW HIGH-VALUE LEAD DETECTED!
👤 Name: György Orosz
🐙 GitHub: https://github.com/oroszgy
🏢 Company: @ec-doris
📍 Location: Budapest, Hungary
👥 Followers: 170
📦 Public Repos: 132
📝 Bio: Freelance NLP engineer
🤖 AI Sales Pitch: György Orosz at @ec-doris has 170 
followers and 132 public repos — they show strong technical 
engagement and would benefit from Yellow.ai's AI automation!