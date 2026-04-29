# deployments

deployment is different from build
must first build then deploy
build is preparing the code, save a distribution in the dist/ folder
deploy is take that distribution, host with a url, then serve to the world, live

## instant rollback
means go back to a previous deployment
need this when current deployment has bugs
need to choose this for that specific deployment in vercel

## preview vs production
both have deployments
preview only for non default branches
production for default branch, go live

# promote
can promote preview to production, default branch doesnt change
just one time change current production deployment to that deployment
when new changes in default branch, trigger new builds, then new production deployment, overwrite temp promoted deployment

# next public api url why empty
this is api url for frontend code to talk to backend app

**why called public**
frontend code is run inside client browser
cant see the env variables in backend server
so backend tell frontend code, it's public, safe to expose api url to browser so frontend code can talk to backend

**api url diff from domain**
user input frontend domain to access our frontend. config this domain in vercel
frontend uses api url to talk to backend

frontend has a domain, backend also has a domain
but user doesnt need to know backend domain

## auto relative routing (dynamic urls)
when vercel deploy next js app,
generate dynamic url for every branch and commit
leave api url empty
frontend code will fall back to relative paths
append relative path to domain currently on
so that api calls can work on production domain, staging domain, temp preview deployment

**diff backend domain has diff api url**

so no need to keep changing fixed api url

## elimiate cors errors
stands for cross origin resource sharing

**a web browser strict security feature**: block frontend on one domain from requesting data from backend on diff domain

*origin means domain*

by keeping frontend and backend on same domain,
and leave api url blank, 

browser treat all api request as internal,
then can bypass cors restriction

## vercel rewrites integration
even if dont need to change domain,
also dont need to have an entire api url,

when combine next js with python backend,
standard practice use `next.config.ts`, rewrite integration rule
routing done by vercel server
no more need api url
just ask for /api