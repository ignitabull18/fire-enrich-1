# 🚀 Fire Enrich - Coolify Deployment Guide

This guide will help you deploy the Fire Enrich application on Coolify using Docker containerization.

## 📋 Prerequisites

- A Coolify server/instance set up and running
- Git repository access (GitHub, GitLab, etc.)
- Required API keys and environment variables (see below)

## 🐳 Docker Configuration

The application has been containerized with the following files:

- **`Dockerfile`**: Multi-stage build optimized for Next.js production
- **`.dockerignore`**: Excludes unnecessary files from Docker build
- **`docker-compose.yml`**: For local testing and development
- **`next.config.ts`**: Updated with `output: 'standalone'` for Docker optimization

## 🔧 Environment Variables

Based on your application structure, you'll likely need to configure these environment variables in Coolify:

### Required API Keys
```bash
# OpenAI API
OPENAI_API_KEY=your_openai_api_key_here

# Firecrawl API (for web scraping)
FIRECRAWL_API_KEY=your_firecrawl_api_key_here
```

### Optional Configuration
```bash
# Node Environment
NODE_ENV=production

# Rate Limiting (if using Upstash Redis)
UPSTASH_REDIS_REST_URL=your_redis_url_here
UPSTASH_REDIS_REST_TOKEN=your_redis_token_here

# Next.js Configuration
NEXT_TELEMETRY_DISABLED=1
```

## 🚀 Deploying on Coolify

### Step 1: Create a New Project
1. Log in to your Coolify dashboard
2. Click "New Project" or "Create Application"
3. Choose "Git Repository" as the source

### Step 2: Repository Configuration
1. Connect your Git repository (GitHub, GitLab, etc.)
2. Select the branch you want to deploy (usually `main` or `master`)
3. Set the **Root Directory** to `/` (root of your repository)

### Step 3: Build Configuration
1. **Build Pack**: Select "Docker"
2. **Dockerfile**: Use `./Dockerfile` (the one we created)
3. **Docker Build Context**: `.` (current directory)

### Step 4: Environment Variables
1. Go to the "Environment Variables" section in your Coolify project
2. Add all the required environment variables listed above
3. Make sure to mark sensitive variables (API keys) as "Secret"

### Step 5: Port Configuration
1. Set the **Port** to `3000` (this is what the app listens on)
2. The Dockerfile already exposes port 3000

### Step 6: Deploy
1. Click "Deploy" to start the deployment process
2. Monitor the build logs for any issues
3. Once deployed, your app will be available at the assigned URL

## 🧪 Local Testing

Before deploying, you can test the Docker build locally:

```bash
# Build the Docker image
docker build -t fire-enrich .

# Run the container
docker run -p 3000:3000 --env-file .env fire-enrich

# Or use docker-compose
docker-compose up --build
```

Create a `.env` file with your environment variables for local testing:
```bash
OPENAI_API_KEY=your_key_here
FIRECRAWL_API_KEY=your_key_here
NODE_ENV=production
```

## 🔍 Troubleshooting

### Common Issues:

1. **Build Failures**:
   - Check that all environment variables are set correctly
   - Ensure your Git repository is accessible
   - Verify the Dockerfile path is correct

2. **Runtime Errors**:
   - Check the application logs in Coolify
   - Verify API keys are valid and not expired
   - Ensure all required environment variables are set

3. **Port Issues**:
   - Make sure port 3000 is configured in Coolify
   - Check that the port isn't blocked by firewalls

### Useful Commands:
```bash
# Check if the container is running
docker ps

# View container logs
docker logs <container_id>

# Test the health of your deployment
curl http://your-coolify-url.com/api/check-env
```

## 📝 Notes

- The Docker build uses multi-stage building for optimal image size
- Static files and assets are properly handled
- The application runs as a non-root user for security
- Hot reloading is disabled in production builds

## 🎯 Next Steps

After successful deployment:
1. Configure your domain/subdomain in Coolify
2. Set up SSL certificates (Coolify handles this automatically)
3. Monitor your application logs and performance
4. Consider setting up automated backups if your app stores data

## 🆘 Support

If you encounter issues:
1. Check the Coolify documentation: https://coolify.io/docs
2. Review the build and runtime logs
3. Ensure all environment variables are correctly configured

Happy deploying! 🚀 