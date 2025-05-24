# Install and Configure Jupyter Notebook in Docker with Password

## Prerequisites
# - Docker must be installed.

# ---------------------------------------
# 1. Generate a Hashed Password for Jupyter Notebook

# Install the required Python package:
pip install jupyter-server

# Run the password generator:
jupyter server password

# You will be prompted to enter and verify your password:
# Enter password: ********
# Verify password: ********

# Example output:
# [JupyterPasswordApp] Wrote hashed password to /home/ryuk/.jupyter/jupyter_server_config.json

# Sample config content:
# {
#   "IdentityProvider": {
#     "hashed_password": "argon2:$argon2id$v=19$m=10240,t=10,p=8$NXBR4EB++sWzXCK6Afddzw$eHPR1jfq9cliQ+R86cNXzlLWoQfY"
#   }
# }

# Copy the value of "hashed_password" and paste it into:
# jupyter_config/jupyter_notebook_config.py

# ---------------------------------------
# 2. Run Jupyter Notebook with Docker Compose

# Navigate to the jupyter-docker folder and run:
docker compose up -d

# Wait for initialization, then open:
# http://<your-ip>:8888
# Enter your password to log in.

# ---------------------------------------
# 3. Add a New Kernel

# Step 1: Exec into the Docker container:
docker exec -it miniconda_jupyter bash

# Step 2: Create a new Conda environment:
conda create -n test python=3.10.16 -y

# Step 3: Activate the environment:
conda activate test

# Step 4: Install kernel support and requirements:
pip install ipykernel
python -m ipykernel install --user --name test --display-name "Python 3.10 (test)"
pip install -r requirements.txt

# ---------------------------------------
# ✅ After Completion
# You will now see "Python 3.10 (test)" as a selectable kernel in Jupyter Notebook.

# NOTE: If the new kernel does not appear, restart the container or your browser session.
