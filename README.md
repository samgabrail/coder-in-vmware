# Detailed End-to-End Workflow with Coder for IT Staff in a VMware Environment

This workflow keeps Coder focused on providing development environments while using Git for feature branch management and promotion, with Jenkins handling the CI/CD process independently for runtime.

## 1. Environment Provisioning
- IT staff logs into Coder web interface with company SSO
- Selects "Create Workspace" in Coder dashboard
- Chooses from Coder templates:
  - Python Web App (Flask/FastAPI)
  - Python Data Analysis (Jupyter)
  - Python Automation Script
- Enters GitHub repo URL or opts to create new repo
- Configures workspace resources (CPU/memory)
- Clicks "Create Workspace"

## 2. Automated Provisioning
- Coder executes its embedded Terraform provider for VMware:
  - Provisions VM in vSphere dev environment
  - Configures networking/storage per template
  - Installs required Python dependencies
- Coder sets up the environment:
  - Clones specified GitHub repo or initializes new one
  - Configures pre-commit hooks and linting
  - Sets up IDE with Python extensions
  - Includes Jenkins pipeline configuration files

## 3. Working Environment
- IT staff accesses workspace through Coder:
  - Web UI with embedded code-server (VS Code in browser)
  - Local VS Code using Coder's remote extension
  - Terminal access for command-line tools
- Environment includes:
  - Persistent workspace state
  - Integrated terminal
  - Pre-configured Python interpreter
  - Template documentation

## 4. Feature Development and Testing
- IT staff creates feature branch in Git (via terminal or VS Code)
  - `git checkout -b feature/new-functionality`
- Makes code changes in Coder workspace
- Tests locally within the workspace
- Commits changes to feature branch
- Pushes to GitHub: `git push origin feature/new-functionality`

## 5. CI Process and Dev Deployment
- GitHub webhook triggers Jenkins pipeline
- Jenkins runs pipeline (configured in workspace template):
  - Tests and validates code
  - Builds application artifacts
  - Uses Terraform to provision/update runtime VM
  - Deploys to dev environment via Ansible playbooks
- IT staff monitors pipeline via Jenkins web UI
- After deployment, IT staff tests application at dev URL

## 6. Promotion to UAT
- IT staff creates pull request in GitHub (via Coder terminal or UI):
  - From feature branch to uat branch
- Code review process (if required)
- Merge to UAT branch triggers Jenkins UAT pipeline:
  - Runs Terraform for UAT infrastructure
  - Deploys to UAT via Ansible
- IT staff monitors deployment via Jenkins

## 7. Production Deployment
- After UAT testing, IT staff creates PR from uat to main branch
- Change approval process occurs in GitHub/ticketing system
- Merge to main triggers production pipeline:
  - Executes Terraform for production environment
  - Deploys via Ansible
- IT staff monitors via Jenkins UI

## 8. Ongoing Development
- Coder workspace remains persistent
- IT staff can:
  - Create new feature branches for additional changes
  - Access deployment logs via Jenkins
  - View application at deployed URLs
  - Continue development in same workspace

## 9. Workspace Management
- Coder provides automatic workspace shutdown policies
- Admin team can manage all environments centrally
- Workspace templates can be updated with new capabilities
- Usage metrics available for optimization