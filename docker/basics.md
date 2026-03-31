# compose
start the container
```bash
docker compose up -d
```

during compose, involve mounting, see `volumes` section

# compose config defined in docker-compose.yml
example, for openclaw sandbox
```yml
# OpenClaw workshop container: agent runs inside the container; host paths are mounted read/write
# only where needed. Execution jail is ./agent_workspace — skills must enforce the same boundary.
services:
  openclaw-agent:
    image: python:3.12-slim-bookworm
    container_name: openclaw-workshop-agent
    working_dir: /app
    env_file:
      - .env
    environment:
      # Explicit jail path inside container (skills resolve against this)
      OPENCLAW_WORKSPACE_ROOT: /workspace
      OPENCLAW_SKILLS_DIR: /app/skills
      OPENCLAW_PROMPTS_DIR: /app/prompts
      OPENCLAW_LOGS_DIR: /var/log/openclaw
    volumes:
      # Execution sandbox — agent file I/O is restricted here by skills + policy
      - ./agent_workspace:/workspace:rw
      # Skill code (read-only in production; rw for local iteration)
      - ./skills:/app/skills:rw
      # Prompts
      - ./prompts:/app/prompts:ro
      # Audit trail (host-backed)
      - ./logs:/var/log/openclaw:rw
      # Optional: mount repo root for workshop exercises
      - ./openclaw.yaml:/app/openclaw.yaml:ro
    # Workshop default: keep container up; replace with your real agent entry point
    command: ["sleep", "infinity"]
    restart: unless-stopped
    security_opt:
      - no-new-privileges:true
    cap_drop:
      - ALL
```
in volumes block,
format = hostPath:containerPath:accessGiven
access is rw or ro

# volumes
volumes = bind mounts = mapped directories = directories or files in host attached at container paths

map host path to repo path
anything written under that path, shows up in host repo, but need write access

# verifying the mounts
```bash
# list all compose-managed containers for the host, where the yml file is located
# can confirm stack is up
docker compose ps
# inspect the bind mounts in container, confirm match volumes block in yml
# inspect returns a lot of things, format flag print only 1 field
# use json, turn mounts objects into json text
# jq is a json processor, make json more readable
# | is pipe, stdout to stdin for next command
docker inspect openclaw-workshop-agent --format '{{json .Mounts}}' | jq
# shell into the container
docker exec -it openclaw-workshop-agent sh
    # using shell, list all the files
    ls -la /workspace /app/skills /app/prompts /var/log/openclaw /app/openclaw.yaml
    # confirm OPENCLAW_WORKSPACE_ROOT
docker exec openclaw-workshop-agent printenv OPENCLAW_WORKSPACE_ROOT
# should print /workspace
```