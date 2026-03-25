# hosting different from domain
domain just an alias to address
need a server which is the host, store all the code

# can self host but
need to run 24/7, if not then go offline, downtime
too slow, home internet connection for download not upload ie send website to clients
security risk, hackers come for your server

# why vercel better than exabytes
| attribute | vercel | exabytes |
| ---------- | --------- | ------------ |
| location | edge network, website copied to many servers globally, so load fast | traditional shared hosting network, only one data center malaysia |
| code updates | connect directly to github, website auto update | manual drag and drop file, via ftp |

# vercel free tier
bandwidth, 100gb / month, ~ 100k visits
compute, 4 hrs active cpu time / month, serverless functions
must be personal, non commercial

# when need pay ($20 / month pro plan)
exceed 100gb
start transactions
have collaborators on vercel

# registry, nameservers, and dns
client sends request to registry to load the domain
registry doesnt know the ip address, redirect client to nameserver of domain
dns is the global network of nameservers, help translate domain into ip address
nameserver return ip address, client can now load


# ds record
delegation signer, part of dnssec, dns security extension
prove dns info coming from nameserver not tampered by man in the middle
registry only has info about domain and its nameserver
ds establish chain of trust between registry and domain