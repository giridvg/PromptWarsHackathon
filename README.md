# AI Travel Planning & Experience Engine

A hackathon-ready, AI-powered travel assistant built with Next.js 14, Tailwind CSS, ShadCN UI, Framer Motion, and OpenAI. Containerized and ready to deploy on Google Cloud Run.

## Features
- **AI-Powered Itineraries:** Instantly generate day-by-day travel plans using OpenAI.
- **Budget Estimation:** Get realistic budget estimates for your trips.
- **Local Insights:** Discover hidden gems and food recommendations.
- **Modern UI:** Premium design with interactive Framer Motion animations and Tailwind CSS.
- **Deploy-Ready:** Fully containerized with Docker for GCP Cloud Run.

## Local Setup

1. **Install Dependencies:**
   \`\`\`bash
   npm install
   \`\`\`

2. **Configure Environment:**
   Create a \`.env.local\` file in the root directory:
   \`\`\`env
   OPENAI_API_KEY=your_openai_api_key_here
   \`\`\`
   *(If you leave this empty, the app will return mock data so your presentation never fails!)*

3. **Run Development Server:**
   \`\`\`bash
   npm run dev
   \`\`\`
   Open [http://localhost:3000](http://localhost:3000)

## Docker Build & Run (Local)

1. **Build the Image:**
   \`\`\`bash
   docker build -t travel-engine .
   \`\`\`

2. **Run the Container:**
   \`\`\`bash
   docker run -p 3000:3000 -e OPENAI_API_KEY="your_api_key" travel-engine
   \`\`\`

## Google Cloud Deployment (Cloud Run)

Follow these steps to deploy your application to GCP:

### 1. Authenticate & Configure GCP
\`\`\`bash
gcloud auth login
gcloud config set project YOUR_PROJECT_ID
\`\`\`

### 2. Enable Required APIs
\`\`\`bash
gcloud services enable artifactregistry.googleapis.com cloudbuild.googleapis.com run.googleapis.com
\`\`\`

### 3. Create an Artifact Registry Repository
\`\`\`bash
gcloud artifacts repositories create travel-repo \\
  --repository-format=docker \\
  --location=us-central1 \\
  --description="Travel Engine Docker repository"
\`\`\`

### 4. Build and Push the Docker Image using Cloud Build
\`\`\`bash
gcloud builds submit --tag us-central1-docker.pkg.dev/YOUR_PROJECT_ID/travel-repo/travel-engine .
\`\`\`

### 5. Deploy to Cloud Run
\`\`\`bash
gcloud run deploy travel-engine \\
  --image us-central1-docker.pkg.dev/YOUR_PROJECT_ID/travel-repo/travel-engine \\
  --platform managed \\
  --region us-central1 \\
  --allow-unauthenticated \\
  --set-env-vars="OPENAI_API_KEY=your_openai_api_key_here"
\`\`\`

You will receive a public URL once the deployment is successful!
