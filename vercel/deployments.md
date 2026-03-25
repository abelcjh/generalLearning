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