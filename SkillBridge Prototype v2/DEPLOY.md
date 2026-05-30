# SkillBridge SA — Deployment Guide

## Deploy to Railway (backend)

1. Push these files to a GitHub repo:
   - SkillBridgeServer.java
   - Procfile
   - .gitignore

2. Go to https://railway.app → New Project → Deploy from GitHub

3. Select your repo — Railway auto-detects Java

4. Railway will:
   - Compile: javac SkillBridgeServer.java
   - Run: java SkillBridgeServer
   - Assign a public URL like: https://skillbridge-sa.up.railway.app

5. Copy that Railway URL

## Connect the frontend

Open index.html — the API URL is already dynamic:
- On localhost → uses http://localhost:8080
- On Railway → uses same-origin (empty string)

So if you host index.html ON Railway too (same project), 
it just works with no changes needed.

## Host frontend on Railway (same project)

Add this line to your Procfile instead:
  web: java SkillBridgeServer

The Java server already serves index.html at GET /
So visiting your Railway URL shows the full site.

## Separate hosting (Netlify frontend + Railway backend)

If you host index.html on Netlify, update this line in index.html:
  const API = window.location.hostname === 'localhost' ...
  : 'https://YOUR-RAILWAY-URL.up.railway.app';

Replace YOUR-RAILWAY-URL with your actual Railway domain.
