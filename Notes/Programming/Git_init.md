### **Steps to Create and Push a Local Repository to GitHub (For a Non-Existing Repo on Local)**

If you have a project on your local machine but **haven’t created a Git repository for it yet**, follow these steps to initialize, commit, and push it to **GitHub**.

---

## **1️⃣ Create a New Repository on GitHub**
1. Go to [GitHub](https://github.com/) and log in.
2. Click the **"+"** icon in the top right and select **"New repository"**.
3. Enter a **repository name**, description, and choose public or private.
4. **Do NOT** initialize with a README, `.gitignore`, or license (we'll add those later).
5. Click **Create repository**.
6. Copy the repository URL (it will look like this):
   - **HTTPS:** `https://github.com/your-username/repo-name.git`
   - **SSH:** `git@github.com:your-username/repo-name.git`

---

## **2️⃣ Initialize Git Locally (If Not Already Initialized)**
If your local project **is not already a Git repo**, open a terminal and navigate to the project directory:
```sh
cd /path/to/your/project
```
Then, initialize Git:
```sh
git init
```
This creates a new `.git` folder to track changes.

---

## **3️⃣ Add and Commit Files**
To add all files to Git tracking:
```sh
git add .
```
Commit the files:
```sh
git commit -m "Initial commit"
```

---

## **4️⃣ Add the GitHub Remote**
Link your local repository to the remote GitHub repository:
```sh
git remote add origin https://github.com/your-username/repo-name.git
```
If using SSH:
```sh
git remote add origin git@github.com:your-username/repo-name.git
```
Verify the remote URL:
```sh
git remote -v
```

---

## **5️⃣ Push to GitHub**
If the default branch is `main`, push using:
```sh
git branch -M main
git push -u origin main
```
If you're using `master` instead of `main`:
```sh
git push -u origin master
```
The `-u` flag sets the upstream branch for future pushes.

---

## **6️⃣ (Optional) Create and Push Additional Branches**
If you have other branches, switch and push them:
```sh
git checkout -b feature-branch
git push -u origin feature-branch
```

---

## **7️⃣ Verify on GitHub**
Go to your GitHub repository page and refresh. You should see all your files uploaded.

---

### **✅ Summary**
| **Step** | **Command** |
|----------|------------|
| **Initialize Git** | `git init` |
| **Add Files** | `git add .` |
| **Commit Changes** | `git commit -m "Initial commit"` |
| **Set Remote** | `git remote add origin <repo-url>` |
| **Push to GitHub** | `git push -u origin main` |
