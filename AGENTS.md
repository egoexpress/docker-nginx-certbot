# Docker Nginx Certbot - Agent Guidelines

## Build/Test Commands
- `docker-compose up -d` - Start services in production mode
- `docker-compose down` - Stop and remove containers
- `docker-compose logs -f` - View service logs
- `docker-compose ps` - Check service status

## Code Style Guidelines
- Use YAML 2-space indentation for docker-compose.yml
- Environment variables in UPPER_SNAKE_CASE
- Service names in lowercase (web, certbot)
- Volume names in lowercase (html, certbot, certs, conf)
- Use official Docker images with specific tags
- Keep image versions pinned (e.g., nginx:1.29-alpine, certbot/certbot:v5.1.0)
- Use restart: always for production services
- Network mode "host" for direct host network access
- Read-only volume mounts where appropriate (:ro suffix)

## Configuration
- Domain and email configured via .env file
- LETSENCRYPT_HOST and LETSENCRYPT_EMAIL required
- Persistent volumes for certificates, config, and content
- Automated dependency updates via Renovate

## Commit Guidelines
- Use Conventional Commit style: `type(scope): description`
- Types: feat, fix, docs, style, refactor, test, chore
- Push commits immediately to GitHub after creation
- Keep commit messages concise and focused on single changes
- Examples: `feat(nginx): add SSL configuration`, `fix(certbot): update image version`